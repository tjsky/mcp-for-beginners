<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7b4b9bfacd2926725e6f1cda82bc8ff5",
  "translation_date": "2025-07-17T11:22:53+00:00",
  "source_file": "06-CommunityContributions/README.md",
  "language_code": "bg"
}
-->
# Общество и приноси

## Преглед

Този урок се фокусира върху това как да се ангажирате с MCP общността, да допринасяте за MCP екосистемата и да следвате добри практики за съвместна разработка. Разбирането как да участвате в отворени MCP проекти е от съществено значение за тези, които искат да оформят бъдещето на тази технология.

## Учебни цели

Към края на този урок ще можете да:
- Разберете структурата на MCP общността и екосистемата
- Участвате ефективно в MCP форуми и дискусии
- Допринасяте към отворените MCP хранилища
- Създавате и споделяте персонализирани MCP инструменти и сървъри
- Следвате добри практики за разработка и сътрудничество в MCP
- Откривате ресурси и рамки за разработка в MCP общността

## MCP общностна екосистема

MCP екосистемата се състои от различни компоненти и участници, които работят заедно за развитието на протокола.

### Основни компоненти на общността

1. **Основни поддръжници на протокола**: Официалната [Model Context Protocol GitHub организация](https://github.com/modelcontextprotocol) поддържа основните MCP спецификации и референтни реализации
2. **Разработчици на инструменти**: Индивиди и екипи, които създават MCP инструменти и сървъри
3. **Доставчици на интеграции**: Компании, които интегрират MCP в своите продукти и услуги
4. **Крайни потребители**: Разработчици и организации, които използват MCP в своите приложения
5. **Приносители**: Членове на общността, които допринасят с код, документация или други ресурси

### Ресурси на общността

#### Официални канали

- [MCP GitHub организация](https://github.com/modelcontextprotocol)
- [MCP документация](https://modelcontextprotocol.io/)
- [MCP спецификация](https://modelcontextprotocol.io/docs/specification)
- [GitHub дискусии](https://github.com/orgs/modelcontextprotocol/discussions)
- [Хранилище с примери и сървъри на MCP](https://github.com/modelcontextprotocol/servers)

#### Ресурси, управлявани от общността

- [MCP клиенти](https://modelcontextprotocol.io/clients) - Списък с клиенти, които поддържат MCP интеграции
- [Общностни MCP сървъри](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file#-community-servers) - Разрастващ се списък с MCP сървъри, разработени от общността
- [Awesome MCP сървъри](https://github.com/wong2/awesome-mcp-servers) - Курирана селекция от MCP сървъри
- [PulseMCP](https://www.pulsemcp.com/) - Общностен център и бюлетин за откриване на MCP ресурси
- [Discord сървър](https://discord.gg/jHEGxQu2a5) - Свържете се с MCP разработчици
- SDK реализации за различни езици
- Блог постове и уроци

## Принос към MCP

### Видове приноси

MCP екосистемата приема различни видове приноси:

1. **Кодови приноси**:
   - Подобрения на основния протокол
   - Отстраняване на грешки
   - Имплементации на инструменти и сървъри
   - Клиентски/сървърни библиотеки на различни езици

2. **Документация**:
   - Подобряване на съществуващата документация
   - Създаване на уроци и ръководства
   - Превод на документация
   - Създаване на примери и примерни приложения

3. **Общностна подкрепа**:
   - Отговаряне на въпроси във форуми и дискусии
   - Тестване и докладване на проблеми
   - Организиране на общностни събития
   - Наставничество на нови приносители

### Процес на принос: Основен протокол

За да допринесете към основния MCP протокол или официалните реализации, следвайте принципите от [официалните насоки за принос](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/CONTRIBUTING.md):

1. **Простота и минимализъм**: MCP спецификацията поддържа високи изисквания за добавяне на нови концепции. По-лесно е да се добавят неща към спецификацията, отколкото да се премахват.

2. **Конкретен подход**: Промените в спецификацията трябва да се базират на конкретни предизвикателства при имплементацията, а не на спекулативни идеи.

3. **Етапи на предложение**:
   - Дефиниране: Изследване на проблема, потвърждаване, че и други MCP потребители имат същия проблем
   - Прототипиране: Създаване на примерен вариант и демонстриране на практическото му приложение
   - Писане: Въз основа на прототипа, написване на предложение за спецификация

### Настройка на средата за разработка

```bash
# Fork the repository
git clone https://github.com/YOUR-USERNAME/modelcontextprotocol.git
cd modelcontextprotocol

# Install dependencies
npm install

# For schema changes, validate and generate schema.json:
npm run check:schema:ts
npm run generate:schema

# For documentation changes
npm run check:docs
npm run format

# Preview documentation locally (optional):
npm run serve:docs
```

### Пример: Принос с поправка на грешка

```javascript
// Original code with bug in the typescript-sdk
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Bug: Missing property validation
  // Current implementation:
  const hasName = 'name' in resource;
  const hasSchema = 'schema' in resource;
  
  return hasName && hasSchema;
}

// Fixed implementation in a contribution
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Improved validation
  const hasName = 'name' in resource && typeof (resource as MCPResource).name === 'string';
  const hasSchema = 'schema' in resource && typeof (resource as MCPResource).schema === 'object';
  const hasDescription = !('description' in resource) || typeof (resource as MCPResource).description === 'string';
  
  return hasName && hasSchema && hasDescription;
}
```

### Пример: Принос с нов инструмент към стандартната библиотека

```python
# Example contribution: A CSV data processing tool for the MCP standard library

from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
import pandas as pd
import io
import json
from typing import Dict, Any, List, Optional

class CsvProcessingTool(Tool):
    """
    Tool for processing and analyzing CSV data.
    
    This tool allows models to extract information from CSV files,
    run basic analysis, and convert data between formats.
    """
    
    def get_name(self):
        return "csvProcessor"
        
    def get_description(self):
        return "Processes and analyzes CSV data"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "csvData": {
                    "type": "string", 
                    "description": "CSV data as a string"
                },
                "csvUrl": {
                    "type": "string",
                    "description": "URL to a CSV file (alternative to csvData)"
                },
                "operation": {
                    "type": "string",
                    "enum": ["summary", "filter", "transform", "convert"],
                    "description": "Operation to perform on the CSV data"
                },
                "filterColumn": {
                    "type": "string",
                    "description": "Column to filter by (for filter operation)"
                },
                "filterValue": {
                    "type": "string",
                    "description": "Value to filter for (for filter operation)"
                },
                "outputFormat": {
                    "type": "string",
                    "enum": ["json", "csv", "markdown"],
                    "default": "json",
                    "description": "Output format for the processed data"
                }
            },
            "oneOf": [
                {"required": ["csvData", "operation"]},
                {"required": ["csvUrl", "operation"]}
            ]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            operation = request.parameters.get("operation")
            output_format = request.parameters.get("outputFormat", "json")
            
            # Get CSV data from either direct data or URL
            df = await self._get_dataframe(request)
            
            # Process based on requested operation
            result = {}
            
            if operation == "summary":
                result = self._generate_summary(df)
            elif operation == "filter":
                column = request.parameters.get("filterColumn")
                value = request.parameters.get("filterValue")
                if not column:
                    raise ToolExecutionException("filterColumn is required for filter operation")
                result = self._filter_data(df, column, value)
            elif operation == "transform":
                result = self._transform_data(df, request.parameters)
            elif operation == "convert":
                result = self._convert_format(df, output_format)
            else:
                raise ToolExecutionException(f"Unknown operation: {operation}")
            
            return ToolResponse(result=result)
        
        except Exception as e:
            raise ToolExecutionException(f"CSV processing failed: {str(e)}")
    
    async def _get_dataframe(self, request: ToolRequest) -> pd.DataFrame:
        """Gets a pandas DataFrame from either CSV data or URL"""
        if "csvData" in request.parameters:
            csv_data = request.parameters.get("csvData")
            return pd.read_csv(io.StringIO(csv_data))
        elif "csvUrl" in request.parameters:
            csv_url = request.parameters.get("csvUrl")
            return pd.read_csv(csv_url)
        else:
            raise ToolExecutionException("Either csvData or csvUrl must be provided")
    
    def _generate_summary(self, df: pd.DataFrame) -> Dict[str, Any]:
        """Generates a summary of the CSV data"""
        return {
            "columns": df.columns.tolist(),
            "rowCount": len(df),
            "columnCount": len(df.columns),
            "numericColumns": df.select_dtypes(include=['number']).columns.tolist(),
            "categoricalColumns": df.select_dtypes(include=['object']).columns.tolist(),
            "sampleRows": json.loads(df.head(5).to_json(orient="records")),
            "statistics": json.loads(df.describe().to_json())
        }
    
    def _filter_data(self, df: pd.DataFrame, column: str, value: str) -> Dict[str, Any]:
        """Filters the DataFrame by a column value"""
        if column not in df.columns:
            raise ToolExecutionException(f"Column '{column}' not found")
            
        filtered_df = df[df[column].astype(str).str.contains(value)]
        
        return {
            "originalRowCount": len(df),
            "filteredRowCount": len(filtered_df),
            "data": json.loads(filtered_df.to_json(orient="records"))
        }
    
    def _transform_data(self, df: pd.DataFrame, params: Dict[str, Any]) -> Dict[str, Any]:
        """Transforms the data based on parameters"""
        # Implementation would include various transformations
        return {
            "status": "success",
            "message": "Transformation applied"
        }
    
    def _convert_format(self, df: pd.DataFrame, format: str) -> Dict[str, Any]:
        """Converts the DataFrame to different formats"""
        if format == "json":
            return {
                "data": json.loads(df.to_json(orient="records")),
                "format": "json"
            }
        elif format == "csv":
            return {
                "data": df.to_csv(index=False),
                "format": "csv"
            }
        elif format == "markdown":
            return {
                "data": df.to_markdown(),
                "format": "markdown"
            }
        else:
            raise ToolExecutionException(f"Unsupported output format: {format}")
```

### Насоки за принос

За да направите успешен принос към MCP проекти:

1. **Започнете с малко**: Започнете с документация, поправки на грешки или малки подобрения
2. **Следвайте стиловия гид**: Спазвайте стила на кодиране и конвенциите на проекта
3. **Пишете тестове**: Включете модулни тестове за вашите кодови приноси
4. **Документирайте работата си**: Добавете ясна документация за нови функции или промени
5. **Подавайте целенасочени PR**: Поддържайте pull request-ите фокусирани върху един проблем или функция
6. **Взаимодействайте с обратната връзка**: Бъдете отзивчиви към коментари по вашите приноси

### Примерен работен процес за принос

```bash
# Clone the repository
git clone https://github.com/modelcontextprotocol/typescript-sdk.git
cd typescript-sdk

# Create a new branch for your contribution
git checkout -b feature/my-contribution

# Make your changes
# ...

# Run tests to ensure your changes don't break existing functionality
npm test

# Commit your changes with a descriptive message
git commit -am "Fix validation in resource handler"

# Push your branch to your fork
git push origin feature/my-contribution

# Create a pull request from your branch to the main repository
# Then engage with feedback and iterate on your PR as needed
```

## Създаване и споделяне на MCP сървъри

Един от най-ценните начини да допринесете за MCP екосистемата е чрез създаване и споделяне на персонализирани MCP сървъри. Общността вече е разработила стотици сървъри за различни услуги и случаи на употреба.

### Рамки за разработка на MCP сървъри

Налични са няколко рамки, които улесняват разработката на MCP сървъри:

1. **Официални SDK**:
   - [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
   - [Python SDK](https://github.com/modelcontextprotocol/python-sdk)
   - [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk)
   - [Go SDK](https://github.com/modelcontextprotocol/go-sdk)
   - [Java SDK](https://github.com/modelcontextprotocol/java-sdk)
   - [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk)

2. **Общностни рамки**:
   - [MCP-Framework](https://mcp-framework.com/) - Създавайте MCP сървъри с елегантност и бързина на TypeScript
   - [MCP Declarative Java SDK](https://github.com/codeboyzhou/mcp-declarative-java-sdk) - MCP сървъри с анотации на Java
   - [Quarkus MCP Server SDK](https://github.com/quarkiverse/quarkus-mcp-server) - Java рамка за MCP сървъри
   - [Next.js MCP Server Template](https://github.com/vercel-labs/mcp-for-next.js) - Стартов проект за MCP сървъри с Next.js

### Разработка на споделими инструменти

#### .NET пример: Създаване на споделим пакет с инструменти

```csharp
// Create a new .NET library project
// dotnet new classlib -n McpFinanceTools

using Microsoft.Mcp.Tools;
using System.Threading.Tasks;
using System.Net.Http;
using System.Text.Json;

namespace McpFinanceTools
{
    // Stock quote tool
    public class StockQuoteTool : IMcpTool
    {
        private readonly HttpClient _httpClient;
        
        public StockQuoteTool(HttpClient httpClient = null)
        {
            _httpClient = httpClient ?? new HttpClient();
        }
        
        public string Name => "stockQuote";
        public string Description => "Gets current stock quotes for specified symbols";
        
        public object GetSchema()
        {
            return new {
                type = "object",
                properties = new {
                    symbol = new { 
                        type = "string",
                        description = "Stock symbol (e.g., MSFT, AAPL)" 
                    },
                    includeHistory = new { 
                        type = "boolean",
                        description = "Whether to include historical data",
                        default = false
                    }
                },
                required = new[] { "symbol" }
            };
        }
        
        public async Task<ToolResponse> ExecuteAsync(ToolRequest request)
        {
            // Extract parameters
            string symbol = request.Parameters.GetProperty("symbol").GetString();
            bool includeHistory = false;
            
            if (request.Parameters.TryGetProperty("includeHistory", out var historyProp))
            {
                includeHistory = historyProp.GetBoolean();
            }
            
            // Call external API (example)
            var quoteResult = await GetStockQuoteAsync(symbol);
            
            // Add historical data if requested
            if (includeHistory)
            {
                var historyData = await GetStockHistoryAsync(symbol);
                quoteResult.Add("history", historyData);
            }
            
            // Return formatted result
            return new ToolResponse {
                Result = JsonSerializer.SerializeToElement(quoteResult)
            };
        }
        
        private async Task<Dictionary<string, object>> GetStockQuoteAsync(string symbol)
        {
            // Implementation would call a real stock API
            // This is a simplified example
            return new Dictionary<string, object>
            {
                ["symbol"] = symbol,
                ["price"] = 123.45,
                ["change"] = 2.5,
                ["percentChange"] = 1.2,
                ["lastUpdated"] = DateTime.UtcNow
            };
        }
        
        private async Task<object> GetStockHistoryAsync(string symbol)
        {
            // Implementation would get historical data
            // Simplified example
            return new[]
            {
                new { date = DateTime.Now.AddDays(-7).Date, price = 120.25 },
                new { date = DateTime.Now.AddDays(-6).Date, price = 122.50 },
                new { date = DateTime.Now.AddDays(-5).Date, price = 121.75 }
                // More historical data...
            };
        }
    }
}

// Create package and publish to NuGet
// dotnet pack -c Release
// dotnet nuget push bin/Release/McpFinanceTools.1.0.0.nupkg -s https://api.nuget.org/v3/index.json -k YOUR_API_KEY
```

#### Java пример: Създаване на Maven пакет за инструменти

```java
// pom.xml configuration for a shareable MCP tool package
<!-- 
<project>
    <groupId>com.example</groupId>
    <artifactId>mcp-weather-tools</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <dependency>
            <groupId>com.mcp</groupId>
            <artifactId>mcp-server</artifactId>
            <version>1.0.0</version>
        </dependency>
    </dependencies>
    
    <distributionManagement>
        <repository>
            <id>github</id>
            <name>GitHub Packages</name>
            <url>https://maven.pkg.github.com/username/mcp-weather-tools</url>
        </repository>
    </distributionManagement>
</project>
-->

package com.example.mcp.weather;

import com.mcp.tools.Tool;
import com.mcp.tools.ToolRequest;
import com.mcp.tools.ToolResponse;
import com.mcp.tools.ToolExecutionException;

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.HashMap;
import java.util.Map;

public class WeatherForecastTool implements Tool {
    private final HttpClient httpClient;
    private final String apiKey;
    
    public WeatherForecastTool(String apiKey) {
        this.httpClient = HttpClient.newHttpClient();
        this.apiKey = apiKey;
    }
    
    @Override
    public String getName() {
        return "weatherForecast";
    }
    
    @Override
    public String getDescription() {
        return "Gets weather forecast for a specified location";
    }
    
    @Override
    public Object getSchema() {
        Map<String, Object> schema = new HashMap<>();
        // Schema definition...
        return schema;
    }
    
    @Override
    public ToolResponse execute(ToolRequest request) {
        try {
            String location = request.getParameters().get("location").asText();
            int days = request.getParameters().has("days") ? 
                request.getParameters().get("days").asInt() : 3;
            
            // Call weather API
            Map<String, Object> forecast = getForecast(location, days);
            
            // Build response
            return new ToolResponse.Builder()
                .setResult(forecast)
                .build();
        } catch (Exception ex) {
            throw new ToolExecutionException("Weather forecast failed: " + ex.getMessage(), ex);
        }
    }
    
    private Map<String, Object> getForecast(String location, int days) {
        // Implementation would call weather API
        // Simplified example
        Map<String, Object> result = new HashMap<>();
        // Add forecast data...
        return result;
    }
}

// Build and publish using Maven
// mvn clean package
// mvn deploy
```

#### Python пример: Публикуване на PyPI пакет

```python
# Directory structure for a PyPI package:
# mcp_nlp_tools/
# ├── LICENSE
# ├── README.md
# ├── setup.py
# ├── mcp_nlp_tools/
# │   ├── __init__.py
# │   ├── sentiment_tool.py
# │   └── translation_tool.py

# Example setup.py
"""
from setuptools import setup, find_packages

setup(
    name="mcp_nlp_tools",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[
        "mcp_server>=1.0.0",
        "transformers>=4.0.0",
        "torch>=1.8.0"
    ],
    author="Your Name",
    author_email="your.email@example.com",
    description="MCP tools for natural language processing tasks",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="https://github.com/username/mcp_nlp_tools",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    python_requires=">=3.8",
)
"""

# Example NLP tool implementation (sentiment_tool.py)
from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
from transformers import pipeline
import torch

class SentimentAnalysisTool(Tool):
    """MCP tool for sentiment analysis of text"""
    
    def __init__(self, model_name="distilbert-base-uncased-finetuned-sst-2-english"):
        # Load the sentiment analysis model
        self.sentiment_analyzer = pipeline("sentiment-analysis", model=model_name)
    
    def get_name(self):
        return "sentimentAnalysis"
        
    def get_description(self):
        return "Analyzes the sentiment of text, classifying it as positive or negative"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "text": {
                    "type": "string", 
                    "description": "The text to analyze for sentiment"
                },
                "includeScore": {
                    "type": "boolean",
                    "description": "Whether to include confidence scores",
                    "default": True
                }
            },
            "required": ["text"]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            text = request.parameters.get("text")
            include_score = request.parameters.get("includeScore", True)
            
            # Analyze sentiment
            sentiment_result = self.sentiment_analyzer(text)[0]
            
            # Format result
            result = {
                "sentiment": sentiment_result["label"],
                "text": text
            }
            
            if include_score:
                result["score"] = sentiment_result["score"]
            
            # Return result
            return ToolResponse(result=result)
            
        except Exception as e:
            raise ToolExecutionException(f"Sentiment analysis failed: {str(e)}")

# To publish:
# python setup.py sdist bdist_wheel
# python -m twine upload dist/*
```

### Споделяне на добри практики

При споделяне на MCP инструменти с общността:

1. **Пълна документация**:
   - Документирайте целта, употребата и примери
   - Обяснете параметрите и връщаните стойности
   - Документирайте външни зависимости

2. **Обработка на грешки**:
   - Имплементирайте стабилна обработка на грешки
   - Осигурете полезни съобщения за грешки
   - Обработвайте гранични случаи внимателно

3. **Съображения за производителност**:
   - Оптимизирайте за скорост и използване на ресурси
   - Използвайте кеширане, когато е подходящо
   - Помислете за мащабируемост

4. **Сигурност**:
   - Използвайте защитени API ключове и автентикация
   - Валидирайте и почиствайте входните данни
   - Прилагайте ограничение на честотата за външни API повиквания

5. **Тестване**:
   - Включете обширно покритие с тестове
   - Тествайте с различни типове входни данни и гранични случаи
   - Документирайте тестовите процедури

## Сътрудничество в общността и добри практики

Ефективното сътрудничество е ключът към процъфтяваща MCP екосистема.

### Канали за комуникация

- GitHub Issues и дискусии
- Microsoft Tech Community
- Discord и Slack канали
- Stack Overflow (таг: `model-context-protocol` или `mcp`)

### Преглед на код

При преглед на MCP приноси:

1. **Яснота**: Ясен и добре документиран ли е кодът?
2. **Коректност**: Работи ли според очакванията?
3. **Последователност**: Спазва ли конвенциите на проекта?
4. **Пълнота**: Включени ли са тестове и документация?
5. **Сигурност**: Има ли потенциални проблеми със сигурността?

### Съвместимост на версиите

При разработка за MCP:

1. **Версиониране на протокола**: Спазвайте версията на MCP протокола, която вашият инструмент поддържа
2. **Съвместимост с клиенти**: Помислете за обратна съвместимост
3. **Съвместимост със сървъри**: Следвайте насоките за имплементация на сървъри
4. **Счупващи промени**: Ясно документирайте всякакви счупващи промени

## Примерен общностен проект: MCP регистър на инструменти

Важен принос към общността може да бъде разработването на публичен регистър за MCP инструменти.

```python
# Example schema for a community tool registry API

from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel, Field, HttpUrl
from typing import List, Optional
import datetime
import uuid

# Models for the tool registry
class ToolSchema(BaseModel):
    """JSON Schema for a tool"""
    type: str
    properties: dict
    required: List[str] = []

class ToolRegistration(BaseModel):
    """Information for registering a tool"""
    name: str = Field(..., description="Unique name for the tool")
    description: str = Field(..., description="Description of what the tool does")
    version: str = Field(..., description="Semantic version of the tool")
    schema: ToolSchema = Field(..., description="JSON Schema for tool parameters")
    author: str = Field(..., description="Author of the tool")
    repository: Optional[HttpUrl] = Field(None, description="Repository URL")
    documentation: Optional[HttpUrl] = Field(None, description="Documentation URL")
    package: Optional[HttpUrl] = Field(None, description="Package URL")
    tags: List[str] = Field(default_factory=list, description="Tags for categorization")
    examples: List[dict] = Field(default_factory=list, description="Example usage")

class Tool(ToolRegistration):
    """Tool with registry metadata"""
    id: uuid.UUID = Field(default_factory=uuid.uuid4)
    created_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    updated_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    downloads: int = Field(default=0)
    rating: float = Field(default=0.0)
    ratings_count: int = Field(default=0)

# FastAPI application for the registry
app = FastAPI(title="MCP Tool Registry")

# In-memory database for this example
tools_db = {}

@app.post("/tools", response_model=Tool)
async def register_tool(tool: ToolRegistration):
    """Register a new tool in the registry"""
    if tool.name in tools_db:
        raise HTTPException(status_code=400, detail=f"Tool '{tool.name}' already exists")
    
    new_tool = Tool(**tool.dict())
    tools_db[tool.name] = new_tool
    return new_tool

@app.get("/tools", response_model=List[Tool])
async def list_tools(tag: Optional[str] = None):
    """List all registered tools, optionally filtered by tag"""
    if tag:
        return [tool for tool in tools_db.values() if tag in tool.tags]
    return list(tools_db.values())

@app.get("/tools/{tool_name}", response_model=Tool)
async def get_tool(tool_name: str):
    """Get information about a specific tool"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    return tools_db[tool_name]

@app.delete("/tools/{tool_name}")
async def delete_tool(tool_name: str):
    """Delete a tool from the registry"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    del tools_db[tool_name]
    return {"message": f"Tool '{tool_name}' deleted"}
```

## Основни изводи

- MCP общността е разнообразна и приема различни видове приноси
- Приносът към MCP може да варира от подобрения на основния протокол до персонализирани инструменти
- Следването на насоките за принос увеличава шансовете вашият PR да бъде приет
- Създаването и споделянето на MCP инструменти е ценен начин за подобряване на екосистемата
- Сътрудничеството в общността е от съществено значение за растежа и усъвършенстването на MCP

## Упражнение

1. Идентифицирайте област в MCP екосистемата, където можете да допринесете според уменията и интересите си
2. Форкнете MCP хранилището и настройте локална среда за разработка
3. Създайте малко подобрение, поправка на грешка или инструмент, който би бил полезен за общността
4. Документирайте приноса си с подходящи тестове и документация
5. Подайте pull request към съответното хранилище

## Допълнителни ресурси

- [MCP общностни проекти](https://github.com/topics/model-context-protocol)


---

Следва: [Уроци от ранното приемане](../07-LessonsfromEarlyAdoption/README.md)

**Отказ от отговорност**:  
Този документ е преведен с помощта на AI преводаческа услуга [Co-op Translator](https://github.com/Azure/co-op-translator). Въпреки че се стремим към точност, моля, имайте предвид, че автоматизираните преводи могат да съдържат грешки или неточности. Оригиналният документ на неговия роден език трябва да се счита за авторитетен източник. За критична информация се препоръчва професионален човешки превод. Ние не носим отговорност за каквито и да е недоразумения или неправилни тълкувания, произтичащи от използването на този превод.