# Django Notes

- django backendini mobil uygulamalarında kullanabilirsin. mesela, bir android appe django backend kurarak user authentication yapmanın (as an alternative to firebase auth) birkaç adımı var:

    ```python
    # 1
    python3 -m venv django_backend

    # 2
    cd django_backend

    # 3
    source ./bin/activate

    # 4 - gerekli paketleri yükle
    pip install django drf djangorestframework-simplejwt django-cors-headers

    INSTALLED_APPS +=
    'rest_framework',
    'corsheaders',
    'my_backend',

    MIDDLEWARE +=
    'corsheaders.middleware.CorsMiddleware', # at the top

    FILE +=
    CORS_ALLOW_ALL_ORIGINS = True  # only for development

    # 5 - django projesi yarat
    django-admin startproject deneme_proje

    # 6
    cd deneme_proje

    # 7 - app yarat
    python manage.py startapp todo_app

    # 8 - ayarlara uygulamanı ekle
    deneme_proje/settings.py - INSTALLED_APPS içine 'deneme_proje' ekle

    # 9 - migrasyonları yap
    python manage.py migrate

    # 10 - admin yarat
    python manage.py createsuperuser

    # 11 - serveri çalıştır (http://127.0.0.1:8000/)
    python manage.py runserver

    # 14 - settings.py'ye şunu ekle
    REST_FRAMEWORK = {
        'DEFAULT_AUTHENTICATION_CLASSES': (
            'rest_framework_simplejwt.authentication.JWTAuthentication',
        ),
    }

    # 15 - todo_app/ altında serializers.py yarat

    from rest_framework import serializers
    from django.contrib.auth.models import User

    class UserSerializer(serializers.ModelSerializer):
        class Meta:
            model = User
            fields = ('id', 'username', 'password')
            extra_kwargs = {'password': {'write_only': True}}

        def create(self, validated_data):
            user = User.objects.create_user(**validated_data)
            return user

    # 16 - todo_app/views.py yarat

    from rest_framework import generics
    from rest_framework.permissions import AllowAny
    from .serializers import UserSerializer
    from rest_framework_simplejwt.views import TokenObtainPairView, TokenRefreshView
    from django.contrib.auth import get_user_model
    User = get_user_model()

    class RegisterView(generics.CreateAPIView):
        queryset = User.objects.all()
        permission_classes = (AllowAny,)
        serializer_class = UserSerializer

    # 17 - todo_app/urls.py yarat

    from django.urls import path
    from .views import RegisterView
    from rest_framework_simplejwt.views import TokenObtainPairView, TokenRefreshView

    urlpatterns = [
        path('api/register/', RegisterView.as_view(), name='auth_register'),
        path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
        path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
    ]

    # 18 - deneme_proje/urls.py altında

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('todo_app.urls')),  # Include your app URLs
    ]

    # 19 - POSTMAN'da kullanıcı kaydetmeyi test et
    http://127.0.0.1:8000/api/register/ # linkine şu json'i POST'la

    {  "username": "yeniUsername",  "password": "yeniSifre"}

    # 20 - POSTMAN'da kullanıcı bilgi almayı test et

    http://127.0.0.1:8000/api/token/ # linkine şu json'i POST'la

    {  "username": "yeniUsername",  "password": "yeniSifre"} # existing user

    # 21 - POSTMAN'da Refresh JWT token test et

    http://127.0.0.1:8000/api/token/refresh/

    # 22 - appin manifest.xml'de

    <uses-permission android:name="android.permission.INTERNET" /> # <manifest>
    android:usesCleartextTraffic="true" # <application>

    # 23 - backend'de settings.py'de host izinleri ver
    ALLOWED_HOSTS = [
        "localhost",
        "127.0.0.1",
        "10.0.2.2",  # 👈 Add this line
    ]

    # 24 - şimdi uygulamanda Retrofit kullanarak bu API endpointlere istekte
    # bulunabilir, kullanıcı bilgileri alıp (GET) verebilirsin (POST).

    ```

- django backend mantıgını android uygulamanda kurarken bilmen gereken bazı adımlar var. android bir uygulamada django be birkaç parçaya ayrılıyor
    - Data Katmanı → data modellerini ve API arayüzlerini yarattığın kısım. eğer API değişirse sadece burayı güncellemen yeterli.
        - Request ve Responseları simgeleyen data modelleri (LoginRequest / LoginResponse).
        - HTTP endpointlerini simgeleyen arayüzlerin (ApiService with login POST)
    - Repository Katmanı → API ve UI arasındaki aracı. Calls the network, processes the results.
        - login() function
    - ViewModel Katmanı → UI belirler, repository fonksiyonlarını çağırır. StateFlow ya da MutableState kullanarak UI’i değiştirir.
    - UI Katmanı → Ekranların vs.
    - Oturum Yönetim Katmanı → credentialslari SharedPreferences ya da EncryptedStorage’da saklar, bir daha açılışta tekrar login ekranına götürmez. sadece logout diyince gider.
- senin credentials’larin JWT (Json web token) saklanır.

```python
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. # hangi algoritma kullanıldı (i.e hs256)
eyJ1c2VybmFtZSI6ImJ1Z3JhIiwiaWQiOjF9. # payload (contains username, id)
L7bzZSRzXhWlvkaue42IfHF2Yb0gq7x5Y1ZZsyfP9mY # signature
```

bir jwt buna benzer.

- what is REST? Representational State Transfer. webservisleri yazma mimarilerinden biridir. Think of REST like **rules for how web services should communicate** - like a protocol for how your frontend talks to your backend. 6 core’u vardır rest’in
    1. **`client-server`** ayrımı. yani client frontend’den server ise backend’den sorumludur.

    ```python
    [Frontend/Mobile App] ←→ [REST API] ←→ [Database]
         (Client)              (Server)
    ```

    1. **`stateless`** olması. ne demek bu? öncelikle state ne demek ona bakalım. state, iki request arasında serverın senin hakkında tuttugu bilgilere denir. user kaydın, credentialsların vs. karşıtı olan architectural approach **`stateful`** mimarisi. geleneksel web applications bunu takip ediyordu, o da şu demek:

    ```python
    # User logs in
    POST /login
    # Server thinks: "I'll remember John is logged in"
    # Server stores: session_id = "abc123", user = "John"

    # Later, user makes another request
    GET /profile
    # Server thinks: "Let me check... ah yes, John is logged in"
    # Server uses stored session to know who you are
    ```

    ama `stateless` olursa (which is how REST behaves), server her request sonrası bildigi her seyi unutuyor. her request ALL NEEDED vermek zorunda.

    ```python
    # EVERY request includes authentication
    GET /profile
    Headers: Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...
    # Server thinks: "I don't remember you, but this token tells me you're John"

    GET /posts
    Headers: Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...
    # Server thinks: "Again, I don't remember you, but token says you're John"
    ```

    neden stateless daha iyi? çünkü farklı server db’leri üzerinde bir user işlem yapmaya calıstıgı zaman stateful’da bu iş problem yaratır çünkü her server sadece kendi kaydettigi bilgileri bilir. stateless’ta ise her şey her seferinde token içinde gittigi icin sorun cıkmaz.

    1. **`cacheable`** olması, yani bilgileri cachte tutması, böylece 2+ seferde daha hızlı ulaşması
    2. **`uniform interface`** olması yani ortak bir dil takip etmesi api handle ederken
    3. **`layered system`** olması
    4. **`code on demand`** olması

    Rest web interaksiyonunda HTTP mantıgını kullanır, HTTP internetin temelidir. 4 temel HTTP metodu

    - GET → retrieves data
    - POST → creates data
    - PUT → updates data
    - DELETE → deletes data

    bunlar endpoint olarak kullanılır. What is an Endpoint? Endpoint = A specific URL where your API can be accessed to perform a particular function.

    ```python
    Endpoint = Base URL + Path + HTTP Method

    Example:
    https://api.example.com/users/123
    │                         │    │
    │                         │    └── Resource ID
    │                         └────── Path
    └─────────────────────────── Base URL

    With HTTP Method: GET https://api.example.com/users/123
    ```

    URL → Uniform Resource Locator. webde bir şeye ulaşırken kullandıgın tam adres

    URI →

    ROUTE → Pattern that defines which code handles which URL

    ```python
    path('users/<int:pk>/', UserViewSet.as_view({'get': 'retrieve'}))
    #     └──────────────┘
    #     This is the route pattern
    ```

    ENDPOINT → Specific combination of URL + HTTP method

    ```python
    GET    /users/123/     # This is an endpoint
    POST   /users/123/     # This is a DIFFERENT endpoint
    # (same URL but different method)
    ```

- what is CRUD? herhangi bir veri üzerinde gerceklestirebilecegin 4 temel işlem
    - create
    - read
    - update
    - delete

    farklı contekslerde farklı anlamlara gelebilir. mesela SQL (database) baglamında:

    ```python
    # create
    INSERT INTO users (name, email) VALUES ("Bugra", "bugra@hotmail.com")

    # update
    UPDATE users SET email = "bugra@gmail.com" WHERE id = 1

    # read
    SELECT * FROM users WHERE id = 1

    # delete
    DELETE FROM users WHERE id = 1
    ```

    ya da http metotları olarak (RestAPI deniyor)

    ```python
    CREATE: POST   /users/     (Create new user)
    READ:   GET    /users/     (List all users)
    READ:   GET    /users/1/   (Get specific user)
    UPDATE: PUT    /users/1/   (Update entire user)
    UPDATE: PATCH  /users/1/   (Update part of user)
    DELETE: DELETE /users/1/   (Delete user)
    ```

    ya da django modeli olarak

    ```python
    # CREATE
    user = User.objects.create(username='john', email='john@email.com')
    # OR
    user = User(username='john', email='john@email.com')
    user.save()

    # READ
    users = User.objects.all()           # Get all users
    user = User.objects.get(id=1)        # Get specific user
    users = User.objects.filter(is_active=True)  # Get filtered users

    # UPDATE
    user = User.objects.get(id=1)
    user.email = 'newemail@email.com'
    user.save()
    # OR
    User.objects.filter(id=1).update(email='newemail@email.com')

    # DELETE
    user = User.objects.get(id=1)
    user.delete()
    # OR
    User.objects.filter(id=1).delete()

    # and
    class UserViewSet(viewsets.ModelViewSet):
        queryset = User.objects.all().order_by('-date_joined')
        serializer_class = UserSerializer
        permission_classes = [permissions.IsAuthenticated]

    # djangoda bu model sayesinde CRUD operasyonlari otomatik gelir
    # yoksa şöyle yazmak gerekecekti# Without ViewSet (more work!)
    def create_user(request):      # Handle POST
    def list_users(request):       # Handle GET (list)
    def get_user(request, id):     # Handle GET (detail)
    def update_user(request, id):  # Handle PUT/PATCH
    def delete_user(request, id):  # Handle DELETE
    ```

    gerçek hayatta CRUD’u her yerde görürüz, sosyal medyada post atmak bir CREATE işlemidir, feedde gezmek bir READ işlemidir, edit mail bir EDIT işlemidir vs.

- 2** kodluysa OK
4** kodluysa sorun api requestinde
5** kodluysa server gone
-
