# GENERATIVE AI NOTES

- the birth of ai dates back to '50s. 2000lere dogru ML gelişti: artık bilgisayar kendi kendine label-image pairleriyle ögrenebilmeye basladı. 17'de bir ml alttürü olan deeplearning doğdu, neural networkler kullanıldı. 21'de ise generative-ai denilen olay dogdu, gen-ai'da artık kullanıcılar promptlar yoluyla ai'ı kullanip egitebiliyor. LLM'ler gen-ai modelidir.
- LLM nasıl çalışıyor? kelimeleri anlayamadıgı icin aslında bir cümledeki kelimeleri sayılara dönüştürüyor, buna transformer mimarisi deniyor. mesela "what": 2061, "?": 30 gibi. "what?": [2061, 30] vektörüyle calısıyor. kendisi cümle yaratırken hangi sayıların hangi sayılardan önce/sonra geldigi occurence'lar üzerine egitiyor kendini. mesela cümle başında kullanılan are'dan sonra %99.9 7 farklı subject token'dan biri gelmişse kendisi de cümle kurarken öyle kullanıyor. ![resim](https://github.com/bugrahankaramollaoglu/generative-ai-for-beginners/raw/main/01-introduction-to-genai/images/tokenizer-example.png?WT.mc_id=academic-105485-koreyst)

- ama aynı prompt her seferinde aynı cevabı üretmesin diye her zaman most occuring token da seçilmiyor ai tarafından, araya `temperature` dediği bir randomness faktörü de katıyor: creativity.
- Neural networks (and in particular Recurrent Neural Networks – RNNs) significantly enhanced natural language processing, enabling the representation of the meaning of text in a more meaningful way, valuing the context of a word in a sentence.
- the difference between a service and a model. A service is a product that is offered by a Cloud Service Provider, and is often a combination of models, data, and other components. A model is the core component of a service, and is often a foundation model, such as an LLM.
- llms are developed cumulatively, that is, chatgpt-3.5 is used to as the `foundation model` to develop chatgpt-4.
- an AI Agent is a tool that enables you to use LLMs. an Agent consists of
  * environment: agentin çalıştığı ortam, websitesi vs.
  * sensors:
  * actuators: agent'i eyleme geçiren kısım.
- azure ai agent service offers you the chance to create your own ai agent
- e
-
