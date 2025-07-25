<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c3f4ea5732d64bf965e8aa2907759709",
  "translation_date": "2025-07-17T01:56:37+00:00",
  "source_file": "02-Security/mcp-security-best-practices-2025.md",
  "language_code": "ne"
}
-->
# MCP सुरक्षा उत्कृष्ट अभ्यासहरू - जुलाई २०२५ अपडेट

## MCP कार्यान्वयनहरूको लागि व्यापक सुरक्षा उत्कृष्ट अभ्यासहरू

MCP सर्भरहरूसँग काम गर्दा, तपाईंको डेटा, पूर्वाधार, र प्रयोगकर्ताहरूलाई सुरक्षित राख्न यी सुरक्षा उत्कृष्ट अभ्यासहरू पालना गर्नुहोस्:

1. **इनपुट प्रमाणीकरण**: इन्जेक्सन आक्रमण र भ्रमित डिप्युटी समस्याहरूबाट जोगिन सधैं इनपुटहरू प्रमाणीकरण र सफा गर्नुहोस्।
   - सबै उपकरण प्यारामिटरहरूको कडा प्रमाणीकरण लागू गर्नुहोस्
   - अनुरोधहरू अपेक्षित ढाँचामा छन् भनी सुनिश्चित गर्न स्कीमा प्रमाणीकरण प्रयोग गर्नुहोस्
   - प्रशोधन अघि सम्भावित हानिकारक सामग्री फिल्टर गर्नुहोस्

2. **पहुँच नियन्त्रण**: तपाईंको MCP सर्भरको लागि उचित प्रमाणीकरण र प्राधिकरण लागू गर्नुहोस्, सूक्ष्म अनुमति सहित।
   - Microsoft Entra ID जस्ता स्थापित पहिचान प्रदायकहरूसँग OAuth 2.0 प्रयोग गर्नुहोस्
   - MCP उपकरणहरूको लागि भूमिका-आधारित पहुँच नियन्त्रण (RBAC) लागू गर्नुहोस्
   - स्थापित समाधानहरू उपलब्ध हुँदा कहिल्यै कस्टम प्रमाणीकरण लागू नगर्नुहोस्

3. **सुरक्षित सञ्चार**: तपाईंको MCP सर्भरसँग सबै सञ्चारका लागि HTTPS/TLS प्रयोग गर्नुहोस् र संवेदनशील डाटाका लागि थप इन्क्रिप्सन थप्न विचार गर्नुहोस्।
   - जहाँ सम्भव TLS 1.3 कन्फिगर गर्नुहोस्
   - महत्वपूर्ण जडानहरूको लागि प्रमाणपत्र पिनिङ लागू गर्नुहोस्
   - प्रमाणपत्रहरू नियमित रूपमा परिवर्तन गर्नुहोस् र तिनीहरूको वैधता जाँच गर्नुहोस्

4. **दर सीमांकन**: दुरुपयोग, DoS आक्रमणहरू रोक्न र स्रोत उपभोग व्यवस्थापन गर्न दर सीमांकन लागू गर्नुहोस्।
   - अपेक्षित प्रयोग ढाँचाहरूको आधारमा उपयुक्त अनुरोध सीमा सेट गर्नुहोस्
   - अत्यधिक अनुरोधहरूका लागि क्रमिक प्रतिक्रिया लागू गर्नुहोस्
   - प्रमाणीकरण स्थितिको आधारमा प्रयोगकर्ता-विशिष्ट दर सीमाहरू विचार गर्नुहोस्

5. **लगिङ र अनुगमन**: तपाईंको MCP सर्भरमा शंकास्पद गतिविधि अनुगमन गर्नुहोस् र व्यापक अडिट ट्रेलहरू लागू गर्नुहोस्।
   - सबै प्रमाणीकरण प्रयासहरू र उपकरण कलहरू लग गर्नुहोस्
   - शंकास्पद ढाँचाहरूका लागि वास्तविक-समय सचेतना लागू गर्नुहोस्
   - लगहरू सुरक्षित रूपमा भण्डारण गरिएका छन् र छेडछाड गर्न नसकिने सुनिश्चित गर्नुहोस्

6. **सुरक्षित भण्डारण**: संवेदनशील डेटा र प्रमाणपत्रहरूलाई उचित इन्क्रिप्सनका साथ सुरक्षित गर्नुहोस्।
   - सबै गोप्य वस्तुहरूको लागि की भल्ट वा सुरक्षित प्रमाणपत्र भण्डार प्रयोग गर्नुहोस्
   - संवेदनशील डाटाका लागि फिल्ड-स्तर इन्क्रिप्सन लागू गर्नुहोस्
   - इन्क्रिप्सन कुञ्जीहरू र प्रमाणपत्रहरू नियमित रूपमा परिवर्तन गर्नुहोस्

7. **टोकन व्यवस्थापन**: सबै मोडेल इनपुट र आउटपुटहरू प्रमाणीकरण र सफा गरेर टोकन पासथ्रू कमजोरीहरू रोक्नुहोस्।
   - दर्शक दाबीहरूमा आधारित टोकन प्रमाणीकरण लागू गर्नुहोस्
   - तपाईंको MCP सर्भरका लागि स्पष्ट रूपमा जारी नगरिएका टोकनहरू कहिल्यै स्वीकार नगर्नुहोस्
   - उचित टोकन जीवनकाल व्यवस्थापन र परिवर्तन लागू गर्नुहोस्

8. **सेसन व्यवस्थापन**: सेसन हाइज्याकिङ र फिक्सेसन आक्रमणहरू रोक्न सुरक्षित सेसन ह्यान्डलिङ लागू गर्नुहोस्।
   - सुरक्षित, गैर-निर्धारित सेसन ID प्रयोग गर्नुहोस्
   - सेसनहरूलाई प्रयोगकर्ता-विशिष्ट जानकारीसँग बाँध्नुहोस्
   - उचित सेसन समाप्ति र परिवर्तन लागू गर्नुहोस्

9. **उपकरण कार्यान्वयन स्यान्डबक्सिङ**: उपकरण कार्यान्वयनहरूलाई अलग वातावरणमा चलाउनुहोस् ताकि यदि कम्प्रोमाइज भएमा पार्श्वगत सर्नबाट रोक्न सकियोस्।
   - उपकरण कार्यान्वयनका लागि कन्टेनर अलगाव लागू गर्नुहोस्
   - स्रोत समाप्ति आक्रमणहरू रोक्न स्रोत सीमाहरू लागू गर्नुहोस्
   - विभिन्न सुरक्षा डोमेनहरूको लागि अलग कार्यान्वयन सन्दर्भहरू प्रयोग गर्नुहोस्

10. **नियमित सुरक्षा अडिटहरू**: तपाईंको MCP कार्यान्वयन र निर्भरताहरूको आवधिक सुरक्षा समीक्षा गर्नुहोस्।
    - नियमित पेनिट्रेसन परीक्षण तालिका बनाउनुहोस्
    - कमजोरीहरू पत्ता लगाउन स्वचालित स्क्यानिङ उपकरणहरू प्रयोग गर्नुहोस्
    - ज्ञात सुरक्षा समस्याहरू समाधान गर्न निर्भरताहरू अपडेट राख्नुहोस्

11. **सामग्री सुरक्षा फिल्टरिङ**: इनपुट र आउटपुट दुवैका लागि सामग्री सुरक्षा फिल्टरहरू लागू गर्नुहोस्।
    - Azure Content Safety वा समान सेवाहरू प्रयोग गरी हानिकारक सामग्री पत्ता लगाउनुहोस्
    - प्रॉम्प्ट इन्जेक्सन रोक्न प्रॉम्प्ट शिल्ड प्रविधिहरू लागू गर्नुहोस्
    - सम्भावित संवेदनशील डाटा चुहावटका लागि उत्पन्न सामग्री स्क्यान गर्नुहोस्

12. **सप्लाई चेन सुरक्षा**: तपाईंको AI सप्लाई चेनका सबै कम्पोनेन्टहरूको अखण्डता र प्रामाणिकता जाँच गर्नुहोस्।
    - हस्ताक्षर गरिएको प्याकेजहरू प्रयोग गर्नुहोस् र हस्ताक्षरहरू प्रमाणित गर्नुहोस्
    - सफ्टवेयर बिल अफ मटेरियल्स (SBOM) विश्लेषण लागू गर्नुहोस्
    - निर्भरताहरूमा दुर्भावनापूर्ण अपडेटहरूको अनुगमन गर्नुहोस्

13. **उपकरण परिभाषा सुरक्षा**: उपकरण परिभाषा र मेटाडेटालाई सुरक्षित गरेर उपकरण विषाक्तता रोक्नुहोस्।
    - प्रयोग अघि उपकरण परिभाषाहरू प्रमाणीकरण गर्नुहोस्
    - उपकरण मेटाडेटामा अनपेक्षित परिवर्तनहरूको अनुगमन गर्नुहोस्
    - उपकरण परिभाषाहरूको अखण्डता जाँच लागू गर्नुहोस्

14. **गतिशील कार्यान्वयन अनुगमन**: MCP सर्भर र उपकरणहरूको रनटाइम व्यवहार अनुगमन गर्नुहोस्।
    - असामान्यताहरू पत्ता लगाउन व्यवहार विश्लेषण लागू गर्नुहोस्
    - अनपेक्षित कार्यान्वयन ढाँचाहरूका लागि सचेतना सेटअप गर्नुहोस्
    - रनटाइम एप्लिकेशन सेल्फ-प्रोटेक्सन (RASP) प्रविधिहरू प्रयोग गर्नुहोस्

15. **न्यूनतम अधिकारको सिद्धान्त**: MCP सर्भर र उपकरणहरू न्यूनतम आवश्यक अनुमति सहित सञ्चालन गरुन्।
    - प्रत्येक अपरेशनका लागि मात्र आवश्यक विशिष्ट अनुमति दिनुहोस्
    - अनुमति प्रयोग नियमित रूपमा समीक्षा र अडिट गर्नुहोस्
    - प्रशासनिक कार्यहरूको लागि जस्ट-इन-टाइम पहुँच लागू गर्नुहोस्

**अस्वीकरण**:  
यो दस्तावेज AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी शुद्धताका लागि प्रयासरत छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटि वा अशुद्धता हुन सक्छ। मूल दस्तावेज यसको मूल भाषामा नै अधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीका लागि व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार छैनौं।