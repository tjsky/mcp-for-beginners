<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4d3415b9d2bf58bc69be07f945a69e07",
  "translation_date": "2025-07-14T05:58:34+00:00",
  "source_file": "09-CaseStudy/travelagentsample.md",
  "language_code": "pa"
}
-->
# ਕੇਸ ਅਧਿਐਨ: Azure AI Travel Agents – ਰੈਫਰੈਂਸ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ

## ਝਲਕ

[Azure AI Travel Agents](https://github.com/Azure-Samples/azure-ai-travel-agents) ਮਾਈਕ੍ਰੋਸਾਫਟ ਵੱਲੋਂ ਵਿਕਸਿਤ ਇੱਕ ਵਿਸਤ੍ਰਿਤ ਰੈਫਰੈਂਸ ਹੱਲ ਹੈ ਜੋ ਦਿਖਾਉਂਦਾ ਹੈ ਕਿ ਕਿਵੇਂ Model Context Protocol (MCP), Azure OpenAI, ਅਤੇ Azure AI Search ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਬਹੁ-ਏਜੰਟ, AI-ਚਲਿਤ ਯਾਤਰਾ ਯੋਜਨਾ ਬਣਾਉਣ ਵਾਲੀ ਐਪਲੀਕੇਸ਼ਨ ਤਿਆਰ ਕੀਤੀ ਜਾ ਸਕਦੀ ਹੈ। ਇਹ ਪ੍ਰੋਜੈਕਟ ਕਈ AI ਏਜੰਟਾਂ ਦੇ ਸਹਿਯੋਗ, ਉਦਯੋਗਿਕ ਡੇਟਾ ਦੇ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਅਤੇ ਇੱਕ ਸੁਰੱਖਿਅਤ, ਵਧਣਯੋਗ ਪਲੇਟਫਾਰਮ ਪ੍ਰਦਾਨ ਕਰਨ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਅਭਿਆਸਾਂ ਨੂੰ ਦਰਸਾਉਂਦਾ ਹੈ।

## ਮੁੱਖ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ
- **ਬਹੁ-ਏਜੰਟ ਸਹਿਯੋਗ:** MCP ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਵਿਸ਼ੇਸ਼ ਏਜੰਟਾਂ (ਜਿਵੇਂ ਕਿ ਫਲਾਈਟ, ਹੋਟਲ, ਅਤੇ ਯਾਤਰਾ ਏਜੰਟ) ਨੂੰ ਸਹਿਯੋਗੀ ਤਰੀਕੇ ਨਾਲ ਕੰਮ ਕਰਨ ਲਈ ਸਮਨਵਿਤ ਕੀਤਾ ਜਾਂਦਾ ਹੈ ਤਾਂ ਜੋ ਜਟਿਲ ਯਾਤਰਾ ਯੋਜਨਾ ਬਣਾਉਣ ਵਾਲੇ ਕੰਮ ਪੂਰੇ ਹੋ ਸਕਣ।
- **ਉਦਯੋਗਿਕ ਡੇਟਾ ਇੰਟੀਗ੍ਰੇਸ਼ਨ:** Azure AI Search ਅਤੇ ਹੋਰ ਉਦਯੋਗਿਕ ਡੇਟਾ ਸਰੋਤਾਂ ਨਾਲ ਜੁੜ ਕੇ ਯਾਤਰਾ ਸਿਫਾਰਸ਼ਾਂ ਲਈ ਤਾਜ਼ਾ ਅਤੇ ਸਬੰਧਤ ਜਾਣਕਾਰੀ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ।
- **ਸੁਰੱਖਿਅਤ, ਵਧਣਯੋਗ ਆਰਕੀਟੈਕਚਰ:** ਪ੍ਰਮਾਣਿਕਤਾ, ਅਧਿਕਾਰ ਅਤੇ ਵਧਣਯੋਗ ਡਿਪਲੋਇਮੈਂਟ ਲਈ Azure ਸੇਵਾਵਾਂ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ, ਉਦਯੋਗਿਕ ਸੁਰੱਖਿਆ ਦੇ ਸਭ ਤੋਂ ਵਧੀਆ ਅਭਿਆਸਾਂ ਦੇ ਅਨੁਸਾਰ।
- **ਵਧਣਯੋਗ ਟੂਲਿੰਗ:** ਦੁਬਾਰਾ ਵਰਤਣ ਯੋਗ MCP ਟੂਲ ਅਤੇ ਪ੍ਰਾਂਪਟ ਟੈਮਪਲੇਟ ਲਾਗੂ ਕਰਦਾ ਹੈ, ਜੋ ਨਵੇਂ ਖੇਤਰਾਂ ਜਾਂ ਕਾਰੋਬਾਰੀ ਲੋੜਾਂ ਲਈ ਤੇਜ਼ੀ ਨਾਲ ਅਨੁਕੂਲਿਤ ਹੋ ਸਕਦੇ ਹਨ।
- **ਉਪਭੋਗਤਾ ਅਨੁਭਵ:** ਯਾਤਰਾ ਏਜੰਟਾਂ ਨਾਲ ਗੱਲਬਾਤ ਕਰਨ ਲਈ ਇੱਕ ਸੰਵਾਦਾਤਮਕ ਇੰਟਰਫੇਸ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ, ਜੋ Azure OpenAI ਅਤੇ MCP ਨਾਲ ਚਲਾਇਆ ਜਾਂਦਾ ਹੈ।

## ਆਰਕੀਟੈਕਚਰ
![Architecture](https://raw.githubusercontent.com/Azure-Samples/azure-ai-travel-agents/main/docs/ai-travel-agents-architecture-diagram.png)

### ਆਰਕੀਟੈਕਚਰ ਡਾਇਗ੍ਰਾਮ ਦਾ ਵੇਰਵਾ

Azure AI Travel Agents ਹੱਲ ਨੂੰ ਮਾਡਿਊਲਰ, ਵਧਣਯੋਗ ਅਤੇ ਕਈ AI ਏਜੰਟਾਂ ਅਤੇ ਉਦਯੋਗਿਕ ਡੇਟਾ ਸਰੋਤਾਂ ਦੇ ਸੁਰੱਖਿਅਤ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਲਈ ਡਿਜ਼ਾਈਨ ਕੀਤਾ ਗਿਆ ਹੈ। ਮੁੱਖ ਭਾਗ ਅਤੇ ਡੇਟਾ ਫਲੋ ਇਸ ਤਰ੍ਹਾਂ ਹਨ:

- **ਉਪਭੋਗਤਾ ਇੰਟਰਫੇਸ:** ਉਪਭੋਗਤਾ ਸੰਵਾਦਾਤਮਕ UI (ਜਿਵੇਂ ਵੈੱਬ ਚੈਟ ਜਾਂ Teams ਬੋਟ) ਰਾਹੀਂ ਸਿਸਟਮ ਨਾਲ ਗੱਲਬਾਤ ਕਰਦੇ ਹਨ, ਜੋ ਉਪਭੋਗਤਾ ਦੇ ਸਵਾਲ ਭੇਜਦਾ ਅਤੇ ਯਾਤਰਾ ਸਿਫਾਰਸ਼ਾਂ ਪ੍ਰਾਪਤ ਕਰਦਾ ਹੈ।
- **MCP ਸਰਵਰ:** ਕੇਂਦਰੀ ਸਮਨਵਯਕ ਹੈ, ਜੋ ਉਪਭੋਗਤਾ ਦੀਆਂ ਇਨਪੁੱਟਾਂ ਪ੍ਰਾਪਤ ਕਰਦਾ, ਸੰਦਰਭ ਸੰਭਾਲਦਾ ਅਤੇ ਵਿਸ਼ੇਸ਼ ਏਜੰਟਾਂ (ਜਿਵੇਂ FlightAgent, HotelAgent, ItineraryAgent) ਦੀ ਕਾਰਵਾਈਆਂ ਨੂੰ Model Context Protocol ਰਾਹੀਂ ਕੋਆਰਡੀਨੇਟ ਕਰਦਾ ਹੈ।
- **AI ਏਜੰਟ:** ਹਰ ਏਜੰਟ ਇੱਕ ਖਾਸ ਖੇਤਰ (ਫਲਾਈਟ, ਹੋਟਲ, ਯਾਤਰਾ) ਲਈ ਜ਼ਿੰਮੇਵਾਰ ਹੈ ਅਤੇ MCP ਟੂਲ ਵਜੋਂ ਲਾਗੂ ਕੀਤਾ ਗਿਆ ਹੈ। ਏਜੰਟ ਪ੍ਰਾਂਪਟ ਟੈਮਪਲੇਟ ਅਤੇ ਲਾਜਿਕ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਬੇਨਤੀਆਂ ਪ੍ਰਕਿਰਿਆ ਕਰਦੇ ਅਤੇ ਜਵਾਬ ਤਿਆਰ ਕਰਦੇ ਹਨ।
- **Azure OpenAI ਸੇਵਾ:** ਉੱਚ-ਪੱਧਰੀ ਕੁਦਰਤੀ ਭਾਸ਼ਾ ਸਮਝ ਅਤੇ ਉਤਪਾਦਨ ਪ੍ਰਦਾਨ ਕਰਦੀ ਹੈ, ਜੋ ਏਜੰਟਾਂ ਨੂੰ ਉਪਭੋਗਤਾ ਦੀ ਮੁਰਾਦ ਸਮਝਣ ਅਤੇ ਸੰਵਾਦਾਤਮਕ ਜਵਾਬ ਬਣਾਉਣ ਯੋਗ ਬਣਾਉਂਦੀ ਹੈ।
- **Azure AI Search ਅਤੇ ਉਦਯੋਗਿਕ ਡੇਟਾ:** ਏਜੰਟ Azure AI Search ਅਤੇ ਹੋਰ ਉਦਯੋਗਿਕ ਡੇਟਾ ਸਰੋਤਾਂ ਨੂੰ ਪੁੱਛਗਿੱਛ ਕਰਕੇ ਫਲਾਈਟ, ਹੋਟਲ ਅਤੇ ਯਾਤਰਾ ਵਿਕਲਪਾਂ ਬਾਰੇ ਤਾਜ਼ਾ ਜਾਣਕਾਰੀ ਪ੍ਰਾਪਤ ਕਰਦੇ ਹਨ।
- **ਪ੍ਰਮਾਣਿਕਤਾ ਅਤੇ ਸੁਰੱਖਿਆ:** Microsoft Entra ID ਨਾਲ ਇੰਟੀਗ੍ਰੇਟ ਕਰਦਾ ਹੈ ਅਤੇ ਸਾਰੇ ਸਰੋਤਾਂ ਲਈ ਘੱਟੋ-ਘੱਟ ਅਧਿਕਾਰਾਂ ਵਾਲੇ ਪਹੁੰਚ ਨਿਯੰਤਰਣ ਲਾਗੂ ਕਰਦਾ ਹੈ।
- **ਡਿਪਲੋਇਮੈਂਟ:** Azure Container Apps 'ਤੇ ਡਿਪਲੋਇਮੈਂਟ ਲਈ ਡਿਜ਼ਾਈਨ ਕੀਤਾ ਗਿਆ ਹੈ, ਜੋ ਵਧਣਯੋਗਤਾ, ਨਿਗਰਾਨੀ ਅਤੇ ਕਾਰਜਕੁਸ਼ਲਤਾ ਯਕੀਨੀ ਬਣਾਉਂਦਾ ਹੈ।

ਇਹ ਆਰਕੀਟੈਕਚਰ ਕਈ AI ਏਜੰਟਾਂ ਦੀ ਬਿਨਾਂ ਰੁਕਾਵਟ ਸਮਨਵਯਤਾ, ਉਦਯੋਗਿਕ ਡੇਟਾ ਨਾਲ ਸੁਰੱਖਿਅਤ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਅਤੇ ਖੇਤਰ-ਵਿਸ਼ੇਸ਼ AI ਹੱਲਾਂ ਲਈ ਇੱਕ ਮਜ਼ਬੂਤ, ਵਧਣਯੋਗ ਪਲੇਟਫਾਰਮ ਮੁਹੱਈਆ ਕਰਦਾ ਹੈ।

## ਆਰਕੀਟੈਕਚਰ ਡਾਇਗ੍ਰਾਮ ਦੀ ਕਦਮ-ਦਰ-ਕਦਮ ਵਿਆਖਿਆ
ਕਲਪਨਾ ਕਰੋ ਕਿ ਤੁਸੀਂ ਇੱਕ ਵੱਡੀ ਯਾਤਰਾ ਦੀ ਯੋਜਨਾ ਬਣਾ ਰਹੇ ਹੋ ਅਤੇ ਤੁਹਾਡੇ ਕੋਲ ਹਰ ਵਿਸ਼ੇ 'ਤੇ ਮਾਹਿਰ ਸਹਾਇਕਾਂ ਦੀ ਟੀਮ ਹੈ ਜੋ ਤੁਹਾਡੀ ਹਰ ਜਰੂਰਤ ਵਿੱਚ ਮਦਦ ਕਰ ਰਹੀ ਹੈ। Azure AI Travel Agents ਸਿਸਟਮ ਇਸੇ ਤਰ੍ਹਾਂ ਕੰਮ ਕਰਦਾ ਹੈ, ਵੱਖ-ਵੱਖ ਹਿੱਸਿਆਂ (ਜਿਵੇਂ ਟੀਮ ਮੈਂਬਰ) ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਜਿਨ੍ਹਾਂ ਦੀ ਆਪਣੀ ਖਾਸ ਜ਼ਿੰਮੇਵਾਰੀ ਹੁੰਦੀ ਹੈ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਕੰਮ ਕਰਦਾ ਹੈ:

### ਉਪਭੋਗਤਾ ਇੰਟਰਫੇਸ (UI):
ਇਸਨੂੰ ਆਪਣੇ ਯਾਤਰਾ ਏਜੰਟ ਦੇ ਫਰੰਟ ਡੈਸਕ ਵਜੋਂ ਸੋਚੋ। ਇੱਥੇ ਤੁਸੀਂ (ਉਪਭੋਗਤਾ) ਸਵਾਲ ਪੁੱਛਦੇ ਜਾਂ ਬੇਨਤੀਆਂ ਕਰਦੇ ਹੋ, ਜਿਵੇਂ "ਮੈਨੂੰ ਪੈਰਿਸ ਲਈ ਫਲਾਈਟ ਲੱਭੋ।" ਇਹ ਵੈੱਬਸਾਈਟ ਦਾ ਚੈਟ ਵਿੰਡੋ ਜਾਂ ਮੈਸੇਜਿੰਗ ਐਪ ਹੋ ਸਕਦਾ ਹੈ।

### MCP ਸਰਵਰ (ਸਮਨਵਯਕ):
MCP ਸਰਵਰ ਉਸ ਮੈਨੇਜਰ ਵਾਂਗ ਹੈ ਜੋ ਫਰੰਟ ਡੈਸਕ 'ਤੇ ਤੁਹਾਡੀ ਬੇਨਤੀ ਸੁਣਦਾ ਹੈ ਅਤੇ ਫੈਸਲਾ ਕਰਦਾ ਹੈ ਕਿ ਕਿਹੜਾ ਵਿਸ਼ੇਸ਼ਗਿਆ ਇਸ ਹਿੱਸੇ ਨੂੰ ਸੰਭਾਲੇਗਾ। ਇਹ ਤੁਹਾਡੇ ਸੰਵਾਦ ਦਾ ਟ੍ਰੈਕ ਰੱਖਦਾ ਹੈ ਅਤੇ ਯਕੀਨੀ ਬਣਾਉਂਦਾ ਹੈ ਕਿ ਸਭ ਕੁਝ ਠੀਕ ਤਰ੍ਹਾਂ ਚੱਲੇ।

### AI ਏਜੰਟ (ਮਾਹਿਰ ਸਹਾਇਕ):
ਹਰ ਏਜੰਟ ਕਿਸੇ ਖਾਸ ਖੇਤਰ ਦਾ ਮਾਹਿਰ ਹੁੰਦਾ ਹੈ—ਇੱਕ ਫਲਾਈਟਾਂ ਬਾਰੇ ਜਾਣਦਾ ਹੈ, ਦੂਜਾ ਹੋਟਲਾਂ ਬਾਰੇ, ਅਤੇ ਤੀਜਾ ਤੁਹਾਡੀ ਯਾਤਰਾ ਦੀ ਯੋਜਨਾ ਬਣਾਉਣ ਵਿੱਚ ਮਾਹਿਰ। ਜਦੋਂ ਤੁਸੀਂ ਯਾਤਰਾ ਲਈ ਬੇਨਤੀ ਕਰਦੇ ਹੋ, MCP ਸਰਵਰ ਤੁਹਾਡੀ ਬੇਨਤੀ ਸਹੀ ਏਜੰਟ(ਆਂ) ਨੂੰ ਭੇਜਦਾ ਹੈ। ਇਹ ਏਜੰਟ ਆਪਣੀ ਜਾਣਕਾਰੀ ਅਤੇ ਟੂਲਾਂ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਤੁਹਾਡੇ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਵਿਕਲਪ ਲੱਭਦੇ ਹਨ।

### Azure OpenAI ਸੇਵਾ (ਭਾਸ਼ਾ ਮਾਹਿਰ):
ਇਹ ਉਸ ਭਾਸ਼ਾ ਮਾਹਿਰ ਵਾਂਗ ਹੈ ਜੋ ਬਿਲਕੁਲ ਸਮਝਦਾ ਹੈ ਕਿ ਤੁਸੀਂ ਕੀ ਪੁੱਛ ਰਹੇ ਹੋ, ਚਾਹੇ ਤੁਸੀਂ ਕਿਸੇ ਵੀ ਤਰੀਕੇ ਨਾਲ ਪੁੱਛੋ। ਇਹ ਏਜੰਟਾਂ ਨੂੰ ਤੁਹਾਡੀਆਂ ਬੇਨਤੀਆਂ ਸਮਝਣ ਅਤੇ ਕੁਦਰਤੀ, ਸੰਵਾਦਾਤਮਕ ਭਾਸ਼ਾ ਵਿੱਚ ਜਵਾਬ ਦੇਣ ਵਿੱਚ ਮਦਦ ਕਰਦਾ ਹੈ।

### Azure AI Search ਅਤੇ ਉਦਯੋਗਿਕ ਡੇਟਾ (ਜਾਣਕਾਰੀ ਦੀ ਲਾਇਬ੍ਰੇਰੀ):
ਇੱਕ ਵੱਡੀ, ਤਾਜ਼ਾ ਲਾਇਬ੍ਰੇਰੀ ਦੀ ਕਲਪਨਾ ਕਰੋ ਜਿਸ ਵਿੱਚ ਸਾਰੀ ਨਵੀਂ ਯਾਤਰਾ ਜਾਣਕਾਰੀ—ਫਲਾਈਟਾਂ ਦੇ ਸਮਾਂ-ਸੂਚੀ, ਹੋਟਲ ਦੀ ਉਪਲਬਧਤਾ, ਅਤੇ ਹੋਰ—ਮੌਜੂਦ ਹੈ। ਏਜੰਟ ਇਸ ਲਾਇਬ੍ਰੇਰੀ ਨੂੰ ਖੋਜ ਕੇ ਤੁਹਾਡੇ ਲਈ ਸਭ ਤੋਂ ਸਹੀ ਜਵਾਬ ਲੱਭਦੇ ਹਨ।

### ਪ੍ਰਮਾਣਿਕਤਾ ਅਤੇ ਸੁਰੱਖਿਆ (ਸੁਰੱਖਿਆ ਗਾਰਡ):
ਜਿਵੇਂ ਸੁਰੱਖਿਆ ਗਾਰਡ ਜਾਂਚਦਾ ਹੈ ਕਿ ਕੌਣ ਕਿਸ ਖੇਤਰ ਵਿੱਚ ਜਾ ਸਕਦਾ ਹੈ, ਇਹ ਹਿੱਸਾ ਯਕੀਨੀ ਬਣਾਉਂਦਾ ਹੈ ਕਿ ਸਿਰਫ ਅਧਿਕਾਰਤ ਲੋਕ ਅਤੇ ਏਜੰਟ ਹੀ ਸੰਵੇਦਨਸ਼ੀਲ ਜਾਣਕਾਰੀ ਤੱਕ ਪਹੁੰਚ ਸਕਦੇ ਹਨ। ਇਹ ਤੁਹਾਡੇ ਡੇਟਾ ਨੂੰ ਸੁਰੱਖਿਅਤ ਅਤੇ ਨਿੱਜੀ ਰੱਖਦਾ ਹੈ।

### Azure Container Apps 'ਤੇ ਡਿਪਲੋਇਮੈਂਟ (ਇਮਾਰਤ):
ਸਾਰੇ ਇਹ ਸਹਾਇਕ ਅਤੇ ਟੂਲ ਇੱਕ ਸੁਰੱਖਿਅਤ, ਵਧਣਯੋਗ ਇਮਾਰਤ (ਕਲਾਉਡ) ਦੇ ਅੰਦਰ ਮਿਲ ਕੇ ਕੰਮ ਕਰਦੇ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਸਿਸਟਮ ਇੱਕ ਸਮੇਂ ਵਿੱਚ ਬਹੁਤ ਸਾਰੇ ਉਪਭੋਗਤਾਵਾਂ ਨੂੰ ਸੰਭਾਲ ਸਕਦਾ ਹੈ ਅਤੇ ਜਦੋਂ ਵੀ ਤੁਹਾਨੂੰ ਲੋੜ ਹੋਵੇ, ਉਪਲਬਧ ਰਹਿੰਦਾ ਹੈ।

## ਇਹ ਸਾਰਾ ਪ੍ਰਕਿਰਿਆ ਕਿਵੇਂ ਕੰਮ ਕਰਦੀ ਹੈ:

ਤੁਸੀਂ ਫਰੰਟ ਡੈਸਕ (UI) 'ਤੇ ਸਵਾਲ ਪੁੱਛਦੇ ਹੋ।  
ਮੈਨੇਜਰ (MCP ਸਰਵਰ) ਇਹ ਫੈਸਲਾ ਕਰਦਾ ਹੈ ਕਿ ਕਿਹੜਾ ਮਾਹਿਰ (ਏਜੰਟ) ਤੁਹਾਡੀ ਮਦਦ ਕਰੇਗਾ।  
ਮਾਹਿਰ ਭਾਸ਼ਾ ਮਾਹਿਰ (OpenAI) ਦੀ ਮਦਦ ਨਾਲ ਤੁਹਾਡੀ ਬੇਨਤੀ ਸਮਝਦਾ ਹੈ ਅਤੇ ਲਾਇਬ੍ਰੇਰੀ (AI Search) ਵਿੱਚੋਂ ਸਭ ਤੋਂ ਵਧੀਆ ਜਵਾਬ ਲੱਭਦਾ ਹੈ।  
ਸੁਰੱਖਿਆ ਗਾਰਡ (ਪ੍ਰਮਾਣਿਕਤਾ) ਯਕੀਨੀ ਬਣਾਉਂਦਾ ਹੈ ਕਿ ਸਭ ਕੁਝ ਸੁਰੱਖਿਅਤ ਹੈ।  
ਇਹ ਸਾਰਾ ਕੰਮ ਇੱਕ ਭਰੋਸੇਮੰਦ, ਵਧਣਯੋਗ ਇਮਾਰਤ (Azure Container Apps) ਦੇ ਅੰਦਰ ਹੁੰਦਾ ਹੈ, ਤਾਂ ਜੋ ਤੁਹਾਡਾ ਅਨੁਭਵ ਸੁਗਮ ਅਤੇ ਸੁਰੱਖਿਅਤ ਰਹੇ।  
ਇਹ ਟੀਮ ਵਰਕ ਸਿਸਟਮ ਨੂੰ ਤੇਜ਼ੀ ਨਾਲ ਅਤੇ ਸੁਰੱਖਿਅਤ ਤਰੀਕੇ ਨਾਲ ਤੁਹਾਡੀ ਯਾਤਰਾ ਯੋਜਨਾ ਬਣਾਉਣ ਵਿੱਚ ਮਦਦ ਕਰਦਾ ਹੈ, ਬਿਲਕੁਲ ਇੱਕ ਮਾਡਰਨ ਦਫਤਰ ਵਿੱਚ ਮਾਹਿਰ ਯਾਤਰਾ ਏਜੰਟਾਂ ਦੀ ਟੀਮ ਵਾਂਗ!

## ਤਕਨੀਕੀ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ
- **MCP ਸਰਵਰ:** ਮੁੱਖ ਸਮਨਵਯਕ ਲਾਜਿਕ ਨੂੰ ਹੋਸਟ ਕਰਦਾ ਹੈ, ਏਜੰਟ ਟੂਲਾਂ ਨੂੰ ਐਕਸਪੋਜ਼ ਕਰਦਾ ਹੈ ਅਤੇ ਬਹੁ-ਕਦਮੀ ਯਾਤਰਾ ਯੋਜਨਾ ਵਰਕਫਲੋਜ਼ ਲਈ ਸੰਦਰਭ ਸੰਭਾਲਦਾ ਹੈ।
- **ਏਜੰਟ:** ਹਰ ਏਜੰਟ (ਜਿਵੇਂ FlightAgent, HotelAgent) ਆਪਣੇ ਪ੍ਰਾਂਪਟ ਟੈਮਪਲੇਟ ਅਤੇ ਲਾਜਿਕ ਨਾਲ MCP ਟੂਲ ਵਜੋਂ ਲਾਗੂ ਕੀਤਾ ਗਿਆ ਹੈ।
- **Azure ਇੰਟੀਗ੍ਰੇਸ਼ਨ:** ਕੁਦਰਤੀ ਭਾਸ਼ਾ ਸਮਝ ਲਈ Azure OpenAI ਅਤੇ ਡੇਟਾ ਪ੍ਰਾਪਤੀ ਲਈ Azure AI Search ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ।
- **ਸੁਰੱਖਿਆ:** Microsoft Entra ID ਨਾਲ ਇੰਟੀਗ੍ਰੇਟ ਕਰਦਾ ਹੈ ਅਤੇ ਸਾਰੇ ਸਰੋਤਾਂ ਲਈ ਘੱਟੋ-ਘੱਟ ਅਧਿਕਾਰਾਂ ਵਾਲੇ ਪਹੁੰਚ ਨਿਯੰਤਰਣ ਲਾਗੂ ਕਰਦਾ ਹੈ।
- **ਡਿਪਲੋਇਮੈਂਟ:** ਵਧਣਯੋਗਤਾ ਅਤੇ ਕਾਰਜਕੁਸ਼ਲਤਾ ਲਈ Azure Container Apps 'ਤੇ ਡਿਪਲੋਇਮੈਂਟ ਦਾ ਸਮਰਥਨ ਕਰਦਾ ਹੈ।

## ਨਤੀਜੇ ਅਤੇ ਪ੍ਰਭਾਵ
- ਦਰਸਾਉਂਦਾ ਹੈ ਕਿ MCP ਨੂੰ ਕਿਵੇਂ ਕਈ AI ਏਜੰਟਾਂ ਨੂੰ ਇੱਕ ਅਸਲੀ, ਉਤਪਾਦਨ-ਗਰੇਡ ਸੰਦਰਭ ਵਿੱਚ ਸਮਨਵਿਤ ਕਰਨ ਲਈ ਵਰਤਿਆ ਜਾ ਸਕਦਾ ਹੈ।
- ਏਜੰਟ ਕੋਆਰਡੀਨੇਸ਼ਨ, ਡੇਟਾ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਅਤੇ ਸੁਰੱਖਿਅਤ ਡਿਪਲੋਇਮੈਂਟ ਲਈ ਦੁਬਾਰਾ ਵਰਤਣ ਯੋਗ ਪੈਟਰਨ ਪ੍ਰਦਾਨ ਕਰਕੇ ਹੱਲ ਵਿਕਾਸ ਨੂੰ ਤੇਜ਼ ਕਰਦਾ ਹੈ।
- MCP ਅਤੇ Azure ਸੇਵਾਵਾਂ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਖੇਤਰ-ਵਿਸ਼ੇਸ਼, AI-ਚਲਿਤ ਐਪਲੀਕੇਸ਼ਨਾਂ ਦੇ ਨਿਰਮਾਣ ਲਈ ਇੱਕ ਨਕਸ਼ਾ ਵਜੋਂ ਕੰਮ ਕਰਦਾ ਹੈ।

## ਸੰਦਰਭ
- [Azure AI Travel Agents GitHub Repository](https://github.com/Azure-Samples/azure-ai-travel-agents)  
- [Azure OpenAI Service](https://azure.microsoft.com/en-us/products/ai-services/openai-service/)  
- [Azure AI Search](https://azure.microsoft.com/en-us/products/ai-services/ai-search/)  
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)

**ਅਸਵੀਕਾਰੋਪਣ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦਿਤ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਰੱਖੋ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸਮਰਥਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਆਪਣੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਪ੍ਰਮਾਣਿਕ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਅਸੀਂ ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਉਤਪੰਨ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।