services:
  - type: web
    name: lum-api
    runtime: python
    plan: free
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn main:app --host 0.0.0.0 --port $PORT
    envVars:
      - key: GEMINI_API_KEY
        sync: false          # задаётся вручную в дашборде Render (секрет)
      - key: ALLOWED_ORIGINS
        sync: false
      - key: LIGHT_MODEL
        value: gemini-2.5-flash-lite
      - key: POWER_MODEL
        value: gemini-2.5-flash
      - key: LIGHT_FALLBACKS
        value: gemini-2.5-flash
      - key: POWER_FALLBACKS
        value: gemini-2.5-pro
      - key: CHUNK_SIZE
        value: "300"
      - key: TOP_K
        value: "3"
      - key: CHUNK_DELAY
        value: "0.5"
      - key: TYPE_BOOST
        value: "0.25"
