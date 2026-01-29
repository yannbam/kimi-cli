│ ### 4.1 Built-in Tools (Kimi SDK)                                                                                          │
│ **Available through `client.formulas`:**                                                                                   │
│ - **memory**: Persistent conversation storage                                                                              │
│ - **excel**: Excel/CSV file analysis                                                                                       │
│ - **code_runner**: Python code execution (sandboxed)                                                                       │
│ - **quickjs**: JavaScript execution                                                                                        │
│ - **fetch**: URL content extraction                                                                                        │
│ - **web-search**: Real-time search (charged)                                                                               │
│ - **convert**: Unit conversion                                                                                             │
│ - **date**: Date/time processing                                                                                           │
│ - **base64**: Encoding/decoding                                                                                            │
│ - **rethink**: Intelligent reasoning                                                                                       │
│ - **random-choice**: Random selection                                                                                      │
│ - **mew**: Cat meowing and blessings


│ # Example agent specification                                                                                              │
│ name: "code_reviewer"                                                                                                      │
│ system_prompt: |                                                                                                           │
│   You are a code reviewer. Current directory: ${KIMI_WORK_DIR}                                                             │
│   Time: ${KIMI_NOW}                                                                                                        │
│                                                                                                                            │
│   Review code for:                                                                                                         │
│   - Security vulnerabilities                                                                                               │
│   - Performance issues                                                                                                     │
│   - Code style violations                                                                                                  │
│                                                                                                                            │
│ tools:                                                                                                                     │
│   - ReadFile                                                                                                               │
│   - WriteFile                                                                                                              │
│   - bash                                                                                                                   │
│   - grep                                                                                                                   │
│ ```

