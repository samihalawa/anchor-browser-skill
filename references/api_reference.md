## Anchor Browser API OpenAPI Schema

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Anchor Browser API",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://api.anchorbrowser.io/v1"
    }
  ],
  "paths": {
    "/sessions": {
      "post": {
        "summary": "Start a new browser session",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "session": {
                    "type": "object",
                    "properties": {
                      "initial_url": { "type": "string" },
                      "recording": { "type": "object", "properties": { "active": { "type": "boolean" } } },
                      "timeout": { "type": "object", "properties": { "idle_timeout": { "type": "integer" }, "max_duration": { "type": "integer" } } }
                    }
                  },
                  "browser": {
                    "type": "object",
                    "properties": {
                      "headless": { "type": "object", "properties": { "active": { "type": "boolean" } } },
                      "adblock": { "type": "object", "properties": { "active": { "type": "boolean" } } },
                      "popup_blocker": { "type": "object", "properties": { "active": { "type": "boolean" } } },
                      "captcha_solver": { "type": "object", "properties": { "active": { "type": "boolean" } } },
                      "viewport": { "type": "object", "properties": { "width": { "type": "integer" }, "height": { "type": "integer" } } }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Session started successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": { "type": "string" },
                        "cdp_url": { "type": "string" },
                        "live_view_url": { "type": "string" }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sessions/{sessionId}/navigate": {
      "post": {
        "summary": "Navigate to a new URL within the session",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "url": { "type": "string" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Navigation successful" } }
      }
    },
    "/sessions/{sessionId}/screenshot": {
      "get": {
        "summary": "Get a screenshot of the current page",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": { "200": { "description": "Screenshot image data" } }
      }
    },
    "/sessions/{sessionId}/mouse/click": {
      "post": {
        "summary": "Perform a mouse click",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "x": { "type": "integer" },
                  "y": { "type": "integer" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Click successful" } }
      }
    },
    "/sessions/{sessionId}/mouse/double-click": {
      "post": {
        "summary": "Perform a mouse double click",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "x": { "type": "integer" },
                  "y": { "type": "integer" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Double click successful" } }
      }
    },
    "/sessions/{sessionId}/keyboard/type": {
      "post": {
        "summary": "Type text into the browser",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "text": { "type": "string" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Text typed successfully" } }
      }
    },
    "/sessions/{sessionId}/keyboard/shortcut": {
      "post": {
        "summary": "Send a keyboard shortcut",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "keys": { "type": "array", "items": { "type": "string" } }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Shortcut sent successfully" } }
      }
    },
    "/sessions/{sessionId}/scroll": {
      "post": {
        "summary": "Scroll the page",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "x": { "type": "integer" },
                  "y": { "type": "integer" },
                  "delta_y": { "type": "integer" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Scroll successful" } }
      }
    },
    "/sessions/{sessionId}/mouse/drag": {
      "post": {
        "summary": "Perform a drag and drop operation",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "from": { "type": "object", "properties": { "x": { "type": "integer" }, "y": { "type": "integer" } } },
                  "to": { "type": "object", "properties": { "x": { "type": "integer" }, "y": { "type": "integer" } } }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Drag successful" } }
      }
    },
    "/sessions/{sessionId}/clipboard": {
      "get": {
        "summary": "Get clipboard content",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": { "200": { "description": "Clipboard content" } }
      },
      "post": {
        "summary": "Set clipboard content",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "text": { "type": "string" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Clipboard set successfully" } }
      }
    },
    "/ai-tools/web-task": {
      "post": {
        "summary": "Perform a high-level web task using AI",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "session_id": { "type": "string" },
                  "task": { "type": "string" }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Web task initiated",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "taskId": { "type": "string" }
                  }
                }
              }
            }
          }
        }
      }
    },
    "/ai-tools/web-task/{taskId}": {
      "get": {
        "summary": "Poll for web task status",
        "parameters": [
          { "name": "taskId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": {
          "200": {
            "description": "Web task status",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": { "type": "string" }
                  }
                }
              }
            }
          }
        }
      }
    },
    "/tools/webpage-content": {
      "post": {
        "summary": "Get full page HTML/text content",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "session_id": { "type": "string" }
                }
              }
            }
          }
        },
        "responses": { "200": { "description": "Page content" } }
      }
    },
    "/sessions/{sessionId}": {
      "delete": {
        "summary": "End a browser session",
        "parameters": [
          { "name": "sessionId", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": { "200": { "description": "Session ended successfully" } }
      }
    }
  }
}
```
