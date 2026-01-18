# Local LLM & RAG Backend Architecture (FastAPI + MVC)

Bu proje, **yerel LLM (Large Language Model)** modelleri ve **RAG (Retrieval-Augmented Generation)** mimarisini, **ölçeklenebilir ve sürdürülebilir bir Backend servisi** olarak sunmak amacıyla geliştirilmiş bir **bitirme projesidir**.

Proje, eğitim sürecinde incelenen referans bir mimarinin **forklanarak kişiselleştirilmesi** ile oluşturulmuş; mimari yapı analiz edilmiş, yeniden düzenlenmiş ve **kişisel bir LLM backend altyapısı** haline getirilmiştir.

Amaç, mezuniyet sonrasında da geliştirilmeye devam edilebilecek, **“evladiyelik”** bir referans backend mimarisi oluşturmaktır.

---

## 🎯 Projenin Amacı

Bu projenin temel amaçları şunlardır:

- LLM tabanlı servislerin **backend mimarisi içinde doğru şekilde konumlandırılmasını** göstermek
- FastAPI üzerinde **MVC (Model–View–Controller)** mimarisini uygulamak
- RAG (Retrieval-Augmented Generation) akışlarını **modüler bir yapıda** tasarlamak
- Ollama üzerinden **local-first LLM kullanımını** örneklemek
- Request / Response yapılarının **net ve genişletilebilir** şekilde tanımlanmasını sağlamak

Bu proje bir ürün geliştirme çalışması değil, **mimari doğruluğu ve sürdürülebilirliği** ön planda tutan bir **referans uygulamadır**.

---

## 🏗 Mimari Yaklaşım ve Nedenleri

Projede, klasik “spagetti kod” yapıları yerine **katmanlı mimari ve MVC tasarım deseni** tercih edilmiştir.

### Neden MVC?

1.  **Sürdürülebilirlik**
    LLM modeli veya embedding altyapısı değiştirildiğinde (ör. Llama yerine Mistral), Controller katmanına dokunulmadan yalnızca Worker katmanı güncellenebilir.

2.  **Bakım Kolaylığı**
    İş mantığı, API tanımları ve response formatları birbirinden ayrıldığı için kod okunabilirliği ve bakım kolaylığı sağlanır.

3.  **Ölçeklenebilirlik**
    Request ve Response yapıları **Pydantic modelleriyle** standartlaştırılmıştır.

---

## 🔄 Sistem Akışı

```text
Client
  │
  ▼
Controller (API Layer)
  │
  ▼
View (Response Mapping)
  │
  ▼
Worker (Business Logic)
  │
  ▼
LLM / RAG / System Services

```

---

## 🧱 Katmanlar

### Controllers
- API endpoint tanımları  
- Request doğrulama  

### Models
- Pydantic Request / Response şemaları  

### Views
- Response mapping ve formatlama  

### Workers
- LLM çağrıları  
- RAG işlemleri  
- Health-check ve loglama işlemleri  

### Core
- Ortak base sınıflar  
- Registry yapıları  

### Data
- Markdown tabanlı Knowledge Base  
