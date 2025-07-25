<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7b4b9bfacd2926725e6f1cda82bc8ff5",
  "translation_date": "2025-07-17T11:59:56+00:00",
  "source_file": "06-CommunityContributions/README.md",
  "language_code": "hr"
}
-->
# Zajednica i doprinosi

## Pregled

Ova lekcija usredotočuje se na to kako se uključiti u MCP zajednicu, doprinositi MCP ekosustavu i slijediti najbolje prakse za suradnički razvoj. Razumijevanje načina sudjelovanja u open-source MCP projektima ključno je za one koji žele oblikovati budućnost ove tehnologije.

## Ciljevi učenja

Do kraja ove lekcije moći ćete:
- Razumjeti strukturu MCP zajednice i ekosustava
- Učinkovito sudjelovati u MCP forumima i raspravama
- Doprinositi MCP open-source repozitorijima
- Kreirati i dijeliti prilagođene MCP alate i servere
- Slijediti najbolje prakse za MCP razvoj i suradnju
- Otkriti resurse i okvire zajednice za MCP razvoj

## MCP ekosustav zajednice

MCP ekosustav sastoji se od različitih komponenti i sudionika koji zajedno rade na unapređenju protokola.

### Ključne komponente zajednice

1. **Održavatelji osnovnog protokola**: službena [Model Context Protocol GitHub organizacija](https://github.com/modelcontextprotocol) održava osnovne MCP specifikacije i referentne implementacije
2. **Razvijatelji alata**: pojedinci i timovi koji stvaraju MCP alate i servere
3. **Pružatelji integracija**: tvrtke koje integriraju MCP u svoje proizvode i usluge
4. **Krajnji korisnici**: developeri i organizacije koje koriste MCP u svojim aplikacijama
5. **Suradnici**: članovi zajednice koji doprinose kodom, dokumentacijom ili drugim resursima

### Resursi zajednice

#### Službeni kanali

- [MCP GitHub organizacija](https://github.com/modelcontextprotocol)
- [MCP dokumentacija](https://modelcontextprotocol.io/)
- [MCP specifikacija](https://modelcontextprotocol.io/docs/specification)
- [GitHub rasprave](https://github.com/orgs/modelcontextprotocol/discussions)
- [Repozitorij MCP primjera i servera](https://github.com/modelcontextprotocol/servers)

#### Resursi koje vodi zajednica

- [MCP klijenti](https://modelcontextprotocol.io/clients) - Popis klijenata koji podržavaju MCP integracije
- [Zajednički MCP serveri](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file#-community-servers) - Rastući popis MCP servera razvijenih od strane zajednice
- [Awesome MCP serveri](https://github.com/wong2/awesome-mcp-servers) - Kurirani popis MCP servera
- [PulseMCP](https://www.pulsemcp.com/) - Zajednički centar i newsletter za otkrivanje MCP resursa
- [Discord server](https://discord.gg/jHEGxQu2a5) - Povežite se s MCP developerima
- Implementacije SDK-a za različite programske jezike
- Blogovi i tutorijali

## Doprinos MCP-u

### Vrste doprinosa

MCP ekosustav prihvaća različite vrste doprinosa:

1. **Doprinosi kodom**:
   - Unapređenja osnovnog protokola
   - Ispravci grešaka
   - Implementacije alata i servera
   - Klijentske/server biblioteke na različitim jezicima

2. **Dokumentacija**:
   - Poboljšanje postojeće dokumentacije
   - Izrada tutorijala i vodiča
   - Prevođenje dokumentacije
   - Izrada primjera i uzoraka aplikacija

3. **Podrška zajednici**:
   - Odgovaranje na pitanja na forumima i raspravama
   - Testiranje i prijavljivanje problema
   - Organiziranje događaja zajednice
   - Mentorstvo novim suradnicima

### Proces doprinosa: Osnovni protokol

Za doprinos osnovnom MCP protokolu ili službenim implementacijama, slijedite principe iz [službenih smjernica za doprinos](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/CONTRIBUTING.md):

1. **Jednostavnost i minimalizam**: MCP specifikacija postavlja visoke standarde za dodavanje novih koncepata. Lakše je dodati nešto u specifikaciju nego to ukloniti.

2. **Konkretan pristup**: Promjene u specifikaciji trebaju se temeljiti na stvarnim izazovima implementacije, a ne na spekulativnim idejama.

3. **Faze prijedloga**:
   - Definiranje: Istražite problem, provjerite imaju li i drugi MCP korisnici sličan problem
   - Prototip: Izradite primjer rješenja i pokažite njegovu praktičnu primjenu
   - Pisanje: Na temelju prototipa napišite prijedlog specifikacije

### Postavljanje razvojne okoline

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

### Primjer: Doprinos ispravkom greške

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

### Primjer: Doprinos novim alatom u standardnoj biblioteci

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

### Smjernice za doprinos

Za uspješan doprinos MCP projektima:

1. **Počnite s malim stvarima**: Započnite s dokumentacijom, ispravcima grešaka ili manjim poboljšanjima
2. **Slijedite stil vodič**: Pridržavajte se stila kodiranja i konvencija projekta
3. **Pišite testove**: Uključite jedinicne testove za svoje kodne doprinose
4. **Dokumentirajte svoj rad**: Dodajte jasnu dokumentaciju za nove značajke ili promjene
5. **Podnosite ciljani PR**: Držite pull requestove fokusiranima na jedan problem ili značajku
6. **Odgovarajte na povratne informacije**: Budite otvoreni i reagirajte na komentare o svojim doprinosima

### Primjer tijeka rada za doprinos

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

## Kreiranje i dijeljenje MCP servera

Jedan od najvrijednijih načina za doprinos MCP ekosustavu je kreiranje i dijeljenje prilagođenih MCP servera. Zajednica je već razvila stotine servera za različite usluge i slučajeve korištenja.

### Okviri za razvoj MCP servera

Dostupno je nekoliko okvira koji olakšavaju razvoj MCP servera:

1. **Službeni SDK-ovi**:
   - [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
   - [Python SDK](https://github.com/modelcontextprotocol/python-sdk)
   - [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk)
   - [Go SDK](https://github.com/modelcontextprotocol/go-sdk)
   - [Java SDK](https://github.com/modelcontextprotocol/java-sdk)
   - [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk)

2. **Okviri zajednice**:
   - [MCP-Framework](https://mcp-framework.com/) - Izgradite MCP servere elegantno i brzo u TypeScriptu
   - [MCP Declarative Java SDK](https://github.com/codeboyzhou/mcp-declarative-java-sdk) - MCP serveri vođeni anotacijama u Javi
   - [Quarkus MCP Server SDK](https://github.com/quarkiverse/quarkus-mcp-server) - Java okvir za MCP servere
   - [Next.js MCP Server Template](https://github.com/vercel-labs/mcp-for-next.js) - Početni Next.js projekt za MCP servere

### Razvijanje alata za dijeljenje

#### .NET primjer: Kreiranje paketa za dijeljivi alat

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

#### Java primjer: Kreiranje Maven paketa za alate

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

#### Python primjer: Objavljivanje PyPI paketa

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

### Dijeljenje najboljih praksi

Prilikom dijeljenja MCP alata sa zajednicom:

1. **Potpuna dokumentacija**:
   - Dokumentirajte svrhu, upotrebu i primjere
   - Objasnite parametre i povratne vrijednosti
   - Dokumentirajte sve vanjske ovisnosti

2. **Rukovanje greškama**:
   - Implementirajte robusno rukovanje greškama
   - Pružite korisne poruke o greškama
   - Pažljivo obradite rubne slučajeve

3. **Razmatranja performansi**:
   - Optimizirajte za brzinu i korištenje resursa
   - Implementirajte keširanje gdje je prikladno
   - Razmotrite skalabilnost

4. **Sigurnost**:
   - Koristite sigurne API ključeve i autentifikaciju
   - Validirajte i sanitizirajte ulaze
   - Implementirajte ograničenje brzine za vanjske API pozive

5. **Testiranje**:
   - Uključite opsežno testiranje
   - Testirajte s različitim vrstama ulaza i rubnim slučajevima
   - Dokumentirajte testne procedure

## Suradnja zajednice i najbolje prakse

Učinkovita suradnja ključ je uspješnog MCP ekosustava.

### Kanali komunikacije

- GitHub Issues i Discussions
- Microsoft Tech Community
- Discord i Slack kanali
- Stack Overflow (tag: `model-context-protocol` ili `mcp`)

### Pregled koda

Prilikom pregleda MCP doprinosa:

1. **Jasnoća**: Je li kod jasan i dobro dokumentiran?
2. **Ispravnost**: Radi li kako se očekuje?
3. **Dosljednost**: Pridržava li se konvencija projekta?
4. **Potpunost**: Jesu li uključeni testovi i dokumentacija?
5. **Sigurnost**: Postoje li sigurnosni problemi?

### Kompatibilnost verzija

Prilikom razvoja za MCP:

1. **Verzioniranje protokola**: Pridržavajte se verzije MCP protokola koju vaš alat podržava
2. **Kompatibilnost klijenata**: Razmotrite unatrag kompatibilnost
3. **Kompatibilnost servera**: Slijedite smjernice za implementaciju servera
4. **Prekidajuće promjene**: Jasno dokumentirajte sve prekidajuće promjene

## Primjer zajedničkog projekta: MCP registar alata

Važan doprinos zajednici može biti razvoj javnog registra MCP alata.

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

## Ključne poruke

- MCP zajednica je raznolika i prihvaća različite vrste doprinosa
- Doprinos MCP-u može uključivati unapređenja osnovnog protokola do prilagođenih alata
- Slijeđenje smjernica za doprinos povećava šanse da vaš PR bude prihvaćen
- Kreiranje i dijeljenje MCP alata vrijedan je način za unapređenje ekosustava
- Suradnja zajednice ključna je za rast i poboljšanje MCP-a

## Vježba

1. Identificirajte područje u MCP ekosustavu gdje možete doprinijeti prema svojim vještinama i interesima
2. Forkajte MCP repozitorij i postavite lokalnu razvojnu okolinu
3. Kreirajte malo poboljšanje, ispravak greške ili alat koji bi koristio zajednici
4. Dokumentirajte svoj doprinos s odgovarajućim testovima i dokumentacijom
5. Pošaljite pull request u odgovarajući repozitorij

## Dodatni resursi

- [MCP Community Projects](https://github.com/topics/model-context-protocol)


---

Sljedeće: [Lessons from Early Adoption](../07-LessonsfromEarlyAdoption/README.md)

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden korištenjem AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako težimo točnosti, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni ljudski prijevod. Ne snosimo odgovornost za bilo kakve nesporazume ili pogrešna tumačenja koja proizlaze iz korištenja ovog prijevoda.