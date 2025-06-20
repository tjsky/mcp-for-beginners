<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2a58caa6e11faa09470b7f81e6729652",
  "translation_date": "2025-06-18T05:52:49+00:00",
  "source_file": "03-GettingStarted/05-sse-server/solution/dotnet/README.md",
  "language_code": "ko"
}
-->
# 이 샘플 실행하기

## -1- 의존성 설치하기

```bash
dotnet restore
```

## -2- 샘플 실행하기

```bash
dotnet run
```

## -3- 샘플 테스트하기

아래 명령을 실행하기 전에 별도의 터미널을 열어 서버가 계속 실행 중인지 확인하세요.

한 터미널에서 서버가 실행 중일 때, 다른 터미널을 열고 다음 명령어를 실행하세요:

```bash
npx @modelcontextprotocol/inspector http://localhost:3001
```

이렇게 하면 샘플을 테스트할 수 있는 시각적 인터페이스가 포함된 웹 서버가 시작됩니다.

> **SSE**가 전송 유형으로 선택되어 있고, URL이 `http://localhost:3001/sse`.

Once the server is connected: 

- try listing tools and run `add`이며, 인자가 2와 4일 때 결과로 6이 보여야 합니다.
- resources와 resource template로 이동해 "greeting"을 호출하고 이름을 입력하면 입력한 이름이 포함된 인사말을 볼 수 있습니다.

### CLI 모드에서 테스트하기

다음 명령어를 실행하면 바로 CLI 모드로 실행할 수 있습니다:

```bash 
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/list
```

서버에서 사용 가능한 모든 도구 목록이 표시됩니다. 다음과 같은 출력이 보여야 합니다:

```text
{
  "tools": [
    {
      "name": "AddNumbers",
      "description": "Add two numbers together.",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "description": "The first number",
            "type": "integer"
          },
          "b": {
            "description": "The second number",
            "type": "integer"
          }
        },
        "title": "AddNumbers",
        "description": "Add two numbers together.",
        "required": [
          "a",
          "b"
        ]
      }
    }
  ]
}
```

도구를 호출하려면 다음과 같이 입력하세요:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/call --tool-name AddNumbers --tool-arg a=1 --tool-arg b=2
```

다음과 같은 출력이 나타납니다:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> 브라우저보다 CLI 모드에서 inspector를 실행하는 것이 보통 훨씬 빠릅니다.
> inspector에 대해 더 알아보려면 [여기](https://github.com/modelcontextprotocol/inspector)를 참고하세요.

**면책 조항**:  
이 문서는 AI 번역 서비스 [Co-op Translator](https://github.com/Azure/co-op-translator)를 사용하여 번역되었습니다. 정확성을 위해 최선을 다하고 있으나, 자동 번역에는 오류나 부정확성이 포함될 수 있음을 유의해 주시기 바랍니다. 원문은 해당 언어의 원본 문서가 권위 있는 자료로 간주되어야 합니다. 중요한 정보의 경우, 전문적인 인간 번역을 권장합니다. 본 번역 사용으로 인해 발생하는 오해나 잘못된 해석에 대해 당사는 책임을 지지 않습니다.