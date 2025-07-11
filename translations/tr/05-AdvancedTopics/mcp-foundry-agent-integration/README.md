<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0d29a939f59d34de10d14433125ea8f5",
  "translation_date": "2025-07-02T10:14:59+00:00",
  "source_file": "05-AdvancedTopics/mcp-foundry-agent-integration/README.md",
  "language_code": "tr"
}
-->
# Model Context Protocol (MCP) Entegrasyonu Azure AI Foundry ile

Bu rehber, Model Context Protocol (MCP) sunucularının Azure AI Foundry ajanlarıyla nasıl entegre edileceğini göstererek güçlü araç orkestrasyonu ve kurumsal yapay zeka yetenekleri sağlar.

## Giriş

Model Context Protocol (MCP), yapay zeka uygulamalarının dış veri kaynakları ve araçlara güvenli şekilde bağlanmasını sağlayan açık bir standarttır. Azure AI Foundry ile entegre edildiğinde, MCP ajanların çeşitli dış hizmetlere, API'lere ve veri kaynaklarına standart bir şekilde erişip etkileşimde bulunmasını mümkün kılar.

Bu entegrasyon, MCP'nin araç ekosisteminin esnekliğini Azure AI Foundry'nin sağlam ajan altyapısıyla birleştirerek kapsamlı özelleştirme seçenekleri sunan kurumsal düzeyde yapay zeka çözümleri sağlar.

**Not:** MCP'yi Azure AI Foundry Agent Service'de kullanmak istiyorsanız, şu anda yalnızca şu bölgeler desteklenmektedir: westus, westus2, uaenorth, southindia ve switzerlandnorth

## Öğrenme Hedefleri

Bu rehberin sonunda şunları yapabileceksiniz:

- Model Context Protocol'ü ve avantajlarını anlamak
- Azure AI Foundry ajanları için MCP sunucularını kurmak
- MCP araç entegrasyonlu ajanlar oluşturup yapılandırmak
- Gerçek MCP sunucuları kullanarak pratik örnekler uygulamak
- Ajan konuşmalarında araç yanıtlarını ve atıfları yönetmek

## Önkoşullar

Başlamadan önce, şunlara sahip olduğunuzdan emin olun:

- AI Foundry erişimi olan bir Azure aboneliği
- Python 3.10+
- Azure CLI kurulmuş ve yapılandırılmış
- AI kaynakları oluşturmak için uygun izinler

## Model Context Protocol (MCP) Nedir?

Model Context Protocol, yapay zeka uygulamalarının dış veri kaynakları ve araçlara bağlanması için standartlaştırılmış bir yoldur. Temel avantajları şunlardır:

- **Standart Entegrasyon**: Farklı araçlar ve hizmetler arasında tutarlı arayüz
- **Güvenlik**: Güvenli kimlik doğrulama ve yetkilendirme mekanizmaları
- **Esneklik**: Çeşitli veri kaynakları, API'ler ve özel araç desteği
- **Genişletilebilirlik**: Yeni özellikler ve entegrasyonların kolay eklenmesi

## Azure AI Foundry ile MCP Kurulumu

### 1. Ortam Yapılandırması

Öncelikle ortam değişkenlerinizi ve bağımlılıkları ayarlayın:

```python
import os
import time
import json
from azure.ai.agents.models import MessageTextContent, ListSortOrder
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential


### 1. Initialize the AI Project Client

```python
project_client = AIProjectClient(
    endpoint="https://your-project-endpoint.services.ai.azure.com/api/projects/your-project",
    credential=DefaultAzureCredential(),
)
```

### 2. Create an Agent with MCP Tools

Configure an agent with MCP server integration:

```python
with project_client:
    agent = project_client.agents.create_agent(
        model="gpt-4.1-nano", 
        name="mcp_agent", 
        instructions="Yardımcı bir asistansınız. Soruları yanıtlamak için sağlanan araçları kullanın. Kaynaklarınızı mutlaka belirtin.",
        tools=[
            {
                "type": "mcp",
                "server_label": "microsoft_docs",
                "server_url": "https://learn.microsoft.com/api/mcp",
                "require_approval": "never"
            }
        ],
        tool_resources=None
    )
    print(f"Oluşturulan ajan, ajan ID'si: {agent.id}")
```

## MCP Tool Configuration Options

When configuring MCP tools for your agent, you can specify several important parameters:

### Configuration

```python
mcp_tool = {
    "type": "mcp",
    "server_label": "unique_server_name",      # MCP sunucusu için tanımlayıcı
    "server_url": "https://api.example.com/mcp", # MCP sunucu uç noktası
    "require_approval": "never"                 # Onay politikası: şu anda sadece "never" destekleniyor
}
```

## Complete Example: Using Microsoft Learn MCP Server

Here's a complete example that demonstrates creating an agent with MCP integration and processing a conversation:

```python
import time
import json
import os
from azure.ai.agents.models import MessageTextContent, ListSortOrder
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

def create_mcp_agent_example():

    project_client = AIProjectClient(
        endpoint="https://your-endpoint.services.ai.azure.com/api/projects/your-project",
        credential=DefaultAzureCredential(),
    )

    with project_client:
        # MCP araçları ile ajan oluşturma
        agent = project_client.agents.create_agent(
            model="gpt-4.1-nano", 
            name="documentation_assistant", 
            instructions="Microsoft dokümantasyonunda uzman yardımcı bir asistansınız. Doğru ve güncel bilgi aramak için Microsoft Learn MCP sunucusunu kullanın. Kaynaklarınızı her zaman belirtin.",
            tools=[
                {
                    "type": "mcp",
                    "server_label": "mslearn",
                    "server_url": "https://learn.microsoft.com/api/mcp",
                    "require_approval": "never"
                }
            ],
            tool_resources=None
        )
        print(f"Oluşturulan ajan, ajan ID'si: {agent.id}")    
        
        # Konuşma dizisi oluşturma
        thread = project_client.agents.threads.create()
        print(f"Oluşturulan dizin, dizi ID'si: {thread.id}")

        # Mesaj gönderme
        message = project_client.agents.messages.create(
            thread_id=thread.id, 
            role="user", 
            content=".NET MAUI nedir? Xamarin.Forms ile nasıl karşılaştırılır?",
        )
        print(f"Oluşturulan mesaj, mesaj ID'si: {message.id}")

        # Ajanı çalıştırma
        run = project_client.agents.runs.create(thread_id=thread.id, agent_id=agent.id)
        
        # Tamamlanma için bekleme
        while run.status in ["queued", "in_progress", "requires_action"]:
            time.sleep(1)
            run = project_client.agents.runs.get(thread_id=thread.id, run_id=run.id)
            print(f"Çalıştırma durumu: {run.status}")

        # Çalıştırma adımlarını ve araç çağrılarını inceleme
        run_steps = project_client.agents.run_steps.list(thread_id=thread.id, run_id=run.id)
        for step in run_steps:
            print(f"Çalıştırma adımı: {step.id}, durum: {step.status}, tür: {step.type}")
            if step.type == "tool_calls":
                print("Araç çağrısı detayları:")
                for tool_call in step.step_details.tool_calls:
                    print(json.dumps(tool_call.as_dict(), indent=2))

        # Konuşmayı gösterme
        messages = project_client.agents.messages.list(thread_id=thread.id, order=ListSortOrder.ASCENDING)
        for data_point in messages:
            last_message_content = data_point.content[-1]
            if isinstance(last_message_content, MessageTextContent):
                print(f"{data_point.role}: {last_message_content.text.value}")

        return agent.id, thread.id

if __name__ == "__main__":
    create_mcp_agent_example()


## Yaygın Sorun Giderme

### 1. Bağlantı Sorunları
- MCP sunucu URL'sinin erişilebilir olduğunu doğrulayın
- Kimlik doğrulama bilgilerini kontrol edin
- Ağ bağlantısını sağlayın

### 2. Araç Çağrısı Hataları
- Araç argümanları ve biçimlendirmeyi gözden geçirin
- Sunucuya özgü gereksinimleri kontrol edin
- Uygun hata yönetimini uygulayın

### 3. Performans Sorunları
- Araç çağrısı sıklığını optimize edin
- Uygun yerlerde önbellekleme yapın
- Sunucu yanıt sürelerini izleyin

## Sonraki Adımlar

MCP entegrasyonunuzu daha da geliştirmek için:

1. **Özel MCP Sunucuları Keşfedin**: Kendi MCP sunucularınızı kurarak özel veri kaynaklarınızı destekleyin
2. **Gelişmiş Güvenlik Uygulayın**: OAuth2 veya özel kimlik doğrulama mekanizmaları ekleyin
3. **İzleme ve Analitik**: Araç kullanımı için kayıt ve izleme mekanizmaları uygulayın
4. **Çözümünüzü Ölçeklendirin**: Yük dengeleme ve dağıtık MCP sunucu mimarilerini değerlendirin

## Ek Kaynaklar

- [Azure AI Foundry Dokümantasyonu](https://learn.microsoft.com/azure/ai-foundry/)
- [Model Context Protocol Örnekleri](https://learn.microsoft.com/azure/ai-foundry/agents/how-to/tools/model-context-protocol-samples)
- [Azure AI Foundry Ajanları Genel Bakış](https://learn.microsoft.com/azure/ai-foundry/agents/)
- [MCP Spesifikasyonu](https://spec.modelcontextprotocol.io/)

## Destek

Ek destek ve sorular için:
- [Azure AI Foundry dokümantasyonunu](https://learn.microsoft.com/azure/ai-foundry/) inceleyin
- [MCP topluluk kaynaklarına](https://modelcontextprotocol.io/) göz atın

## Sonraki Bölüm

- [6. Topluluk Katkıları](../../06-CommunityContributions/README.md)

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba sarf etsek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Orijinal belge, kendi dilinde yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımı sonucu oluşabilecek yanlış anlamalar veya yorum hatalarından sorumlu değiliz.