# Forus Heavy API - Complete Application Code

## Overview
Forus Heavy API is a modern full-stack AI chat application with dual API integration, featuring React frontend, Express.js backend, real-time WebSocket communication, and advanced AI capabilities.

## Setup Instructions

1. **Initialize Project:**
   ```bash
   npm install
   ```

2. **Environment Variables:**
   Set these in your Replit secrets or .env file:
   - `OPENROUTER_API_KEY_1` - Primary OpenRouter API key
   - `OPENROUTER_API_KEY_2` - Secondary OpenRouter API key (optional)
   - `PORT` - Server port (default: 5000)

3. **Run Application:**
   ```bash
   npm run dev
   ```

---

## Complete File Structure

### Root Configuration Files

#### **package.json**
```json
{
  "name": "rest-express",
  "version": "1.0.0",
  "type": "module",
  "license": "MIT",
  "scripts": {
    "dev": "NODE_ENV=development tsx server/index.ts",
    "build": "vite build && esbuild server/index.ts --platform=node --packages=external --bundle --format=esm --outdir=dist",
    "start": "NODE_ENV=production node dist/index.js",
    "check": "tsc",
    "db:push": "drizzle-kit push"
  },
  "dependencies": {
    "@hookform/resolvers": "^3.10.0",
    "@jridgewell/trace-mapping": "^0.3.25",
    "@neondatabase/serverless": "^0.10.4",
    "@radix-ui/react-accordion": "^1.2.4",
    "@radix-ui/react-alert-dialog": "^1.1.7",
    "@radix-ui/react-aspect-ratio": "^1.1.3",
    "@radix-ui/react-avatar": "^1.1.4",
    "@radix-ui/react-checkbox": "^1.1.5",
    "@radix-ui/react-collapsible": "^1.1.4",
    "@radix-ui/react-context-menu": "^2.2.7",
    "@radix-ui/react-dialog": "^1.1.7",
    "@radix-ui/react-dropdown-menu": "^2.1.7",
    "@radix-ui/react-hover-card": "^1.1.7",
    "@radix-ui/react-label": "^2.1.3",
    "@radix-ui/react-menubar": "^1.1.7",
    "@radix-ui/react-navigation-menu": "^1.2.6",
    "@radix-ui/react-popover": "^1.1.7",
    "@radix-ui/react-progress": "^1.1.3",
    "@radix-ui/react-radio-group": "^1.2.4",
    "@radix-ui/react-scroll-area": "^1.2.4",
    "@radix-ui/react-select": "^2.1.7",
    "@radix-ui/react-separator": "^1.1.3",
    "@radix-ui/react-slider": "^1.2.4",
    "@radix-ui/react-slot": "^1.2.0",
    "@radix-ui/react-switch": "^1.1.4",
    "@radix-ui/react-tabs": "^1.1.4",
    "@radix-ui/react-toast": "^1.2.7",
    "@radix-ui/react-toggle": "^1.1.3",
    "@radix-ui/react-toggle-group": "^1.1.3",
    "@radix-ui/react-tooltip": "^1.2.0",
    "@tanstack/react-query": "^5.60.5",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "cmdk": "^1.1.1",
    "connect-pg-simple": "^10.0.0",
    "date-fns": "^3.6.0",
    "drizzle-orm": "^0.39.1",
    "drizzle-zod": "^0.7.0",
    "embla-carousel-react": "^8.6.0",
    "express": "^4.21.2",
    "express-session": "^1.18.1",
    "framer-motion": "^11.13.1",
    "input-otp": "^1.4.2",
    "lucide-react": "^0.453.0",
    "memorystore": "^1.6.7",
    "nanoid": "^5.1.5",
    "next-themes": "^0.4.6",
    "openai": "^5.12.0",
    "passport": "^0.7.0",
    "passport-local": "^1.0.0",
    "react": "^18.3.1",
    "react-day-picker": "^8.10.1",
    "react-dom": "^18.3.1",
    "react-hook-form": "^7.55.0",
    "react-icons": "^5.4.0",
    "react-resizable-panels": "^2.1.7",
    "recharts": "^2.15.2",
    "tailwind-merge": "^2.6.0",
    "tailwindcss-animate": "^1.0.7",
    "tw-animate-css": "^1.2.5",
    "vaul": "^1.1.2",
    "wouter": "^3.3.5",
    "ws": "^8.18.0",
    "zod": "^3.24.2",
    "zod-validation-error": "^3.4.0"
  },
  "devDependencies": {
    "@replit/vite-plugin-cartographer": "^0.2.8",
    "@replit/vite-plugin-runtime-error-modal": "^0.0.3",
    "@tailwindcss/typography": "^0.5.15",
    "@tailwindcss/vite": "^4.1.3",
    "@types/connect-pg-simple": "^7.0.3",
    "@types/express": "4.17.21",
    "@types/express-session": "^1.18.0",
    "@types/node": "20.16.11",
    "@types/passport": "^1.0.16",
    "@types/passport-local": "^1.0.38",
    "@types/react": "^18.3.11",
    "@types/react-dom": "^18.3.1",
    "@types/ws": "^8.5.13",
    "@vitejs/plugin-react": "^4.3.2",
    "autoprefixer": "^10.4.20",
    "drizzle-kit": "^0.30.4",
    "esbuild": "^0.25.0",
    "postcss": "^8.4.47",
    "tailwindcss": "^3.4.17",
    "tsx": "^4.19.1",
    "typescript": "5.6.3",
    "vite": "^5.4.19"
  },
  "optionalDependencies": {
    "bufferutil": "^4.0.8"
  }
}
```

#### **vite.config.ts**
```typescript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";
import runtimeErrorOverlay from "@replit/vite-plugin-runtime-error-modal";

export default defineConfig({
  plugins: [
    react(),
    runtimeErrorOverlay(),
    ...(process.env.NODE_ENV !== "production" &&
    process.env.REPL_ID !== undefined
      ? [
          await import("@replit/vite-plugin-cartographer").then((m) =>
            m.cartographer(),
          ),
        ]
      : []),
  ],
  resolve: {
    alias: {
      "@": path.resolve(import.meta.dirname, "client", "src"),
      "@shared": path.resolve(import.meta.dirname, "shared"),
      "@assets": path.resolve(import.meta.dirname, "attached_assets"),
    },
  },
  root: path.resolve(import.meta.dirname, "client"),
  build: {
    outDir: path.resolve(import.meta.dirname, "dist/public"),
    emptyOutDir: true,
  },
  server: {
    fs: {
      strict: true,
      deny: ["**/.*"],
    },
  },
});
```

#### **tailwind.config.ts**
```typescript
import type { Config } from "tailwindcss";

export default {
  darkMode: ["class"],
  content: ["./client/index.html", "./client/src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      colors: {
        background: "var(--background)",
        foreground: "var(--foreground)",
        card: {
          DEFAULT: "var(--card)",
          foreground: "var(--card-foreground)",
        },
        popover: {
          DEFAULT: "var(--popover)",
          foreground: "var(--popover-foreground)",
        },
        primary: {
          DEFAULT: "var(--primary)",
          foreground: "var(--primary-foreground)",
        },
        secondary: {
          DEFAULT: "var(--secondary)",
          foreground: "var(--secondary-foreground)",
        },
        muted: {
          DEFAULT: "var(--muted)",
          foreground: "var(--muted-foreground)",
        },
        accent: {
          DEFAULT: "var(--accent)",
          foreground: "var(--accent-foreground)",
        },
        destructive: {
          DEFAULT: "var(--destructive)",
          foreground: "var(--destructive-foreground)",
        },
        border: "var(--border)",
        input: "var(--input)",
        ring: "var(--ring)",
        chart: {
          "1": "var(--chart-1)",
          "2": "var(--chart-2)",
          "3": "var(--chart-3)",
          "4": "var(--chart-4)",
          "5": "var(--chart-5)",
        },
        sidebar: {
          DEFAULT: "var(--sidebar-background)",
          foreground: "var(--sidebar-foreground)",
          primary: "var(--sidebar-primary)",
          "primary-foreground": "var(--sidebar-primary-foreground)",
          accent: "var(--sidebar-accent)",
          "accent-foreground": "var(--sidebar-accent-foreground)",
          border: "var(--sidebar-border)",
          ring: "var(--sidebar-ring)",
        },
      },
      keyframes: {
        "accordion-down": {
          from: {
            height: "0",
          },
          to: {
            height: "var(--radix-accordion-content-height)",
          },
        },
        "accordion-up": {
          from: {
            height: "var(--radix-accordion-content-height)",
          },
          to: {
            height: "0",
          },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate"), require("@tailwindcss/typography")],
} satisfies Config;
```

#### **tsconfig.json**
```json
{
  "compilerOptions": {
    "composite": true,
    "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo",
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": false,
    "noUnusedParameters": false,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./client/src/*"],
      "@shared/*": ["./shared/*"]
    }
  },
  "include": ["vite.config.ts", "client/src", "server", "shared", "*.ts"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

---

## Server Code

### **server/index.ts**
```typescript
import express, { type Request, Response, NextFunction } from "express";
import { registerRoutes } from "./routes";
import { setupVite, serveStatic, log } from "./vite";

// Test API connectivity function
async function testAPIConnectivity() {
  console.log('=== TESTING API CONNECTIVITY ===');
  
  try {
    const response = await fetch('https://openrouter.ai/api/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${process.env.OPENROUTER_API_KEY_1}`,
        'Content-Type': 'application/json',
        'HTTP-Referer': process.env.SITE_URL || 'http://localhost:5000',
        'X-Title': 'Forus Heavy API',
      },
      body: JSON.stringify({
        model: "openai/gpt-4o-mini",
        messages: [{ role: "user", content: "test" }],
        max_tokens: 50,
      }),
    });

    if (response.ok) {
      const data = await response.json();
      console.log('✅ API TEST SUCCESSFUL:', data.choices[0]?.message?.content);
    } else {
      const errorText = await response.text();
      console.error('❌ API TEST FAILED:', response.status, response.statusText, errorText);
    }
  } catch (error) {
    console.error('❌ API TEST ERROR:', error);
  }
}

const app = express();
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.use((req, res, next) => {
  const start = Date.now();
  const path = req.path;
  let capturedJsonResponse: Record<string, any> | undefined = undefined;

  const originalResJson = res.json;
  res.json = function (bodyJson, ...args) {
    capturedJsonResponse = bodyJson;
    return originalResJson.apply(res, [bodyJson, ...args]);
  };

  res.on("finish", () => {
    const duration = Date.now() - start;
    if (path.startsWith("/api")) {
      let logLine = `${req.method} ${path} ${res.statusCode} in ${duration}ms`;
      if (capturedJsonResponse) {
        logLine += ` :: ${JSON.stringify(capturedJsonResponse)}`;
      }

      if (logLine.length > 80) {
        logLine = logLine.slice(0, 79) + "…";
      }

      log(logLine);
    }
  });

  next();
});

(async () => {
  const server = await registerRoutes(app);

  app.use((err: any, _req: Request, res: Response, _next: NextFunction) => {
    const status = err.status || err.statusCode || 500;
    const message = err.message || "Internal Server Error";

    res.status(status).json({ message });
    throw err;
  });

  // importantly only setup vite in development and after
  // setting up all the other routes so the catch-all route
  // doesn't interfere with the other routes
  if (app.get("env") === "development") {
    await setupVite(app, server);
  } else {
    serveStatic(app);
  }

  // ALWAYS serve the app on the port specified in the environment variable PORT
  // Other ports are firewalled. Default to 5000 if not specified.
  // this serves both the API and the client.
  // It is the only port that is not firewalled.
  // Debug environment variables
  console.log('=== ENVIRONMENT DEBUG ===');
  console.log('OPENROUTER_API_KEY_1 exists:', !!process.env.OPENROUTER_API_KEY_1);
  console.log('OPENROUTER_API_KEY_2 exists:', !!process.env.OPENROUTER_API_KEY_2);
  console.log('OPENROUTER_API_KEY_1 length:', process.env.OPENROUTER_API_KEY_1?.length || 0);
  console.log('OPENROUTER_API_KEY_2 length:', process.env.OPENROUTER_API_KEY_2?.length || 0);

  const port = parseInt(process.env.PORT || '5000', 10);
  server.listen({
    port,
    host: "0.0.0.0",
    reusePort: true,
  }, () => {
    log(`serving on port ${port}`);
    
    // Test API connectivity on startup
    testAPIConnectivity();
  });
})();
```

### **server/routes.ts**
```typescript
import type { Express } from "express";
import { createServer, type Server } from "http";
import { WebSocketServer, WebSocket } from "ws";
import { storage } from "./storage";
import { AIService } from "./services/ai-service";
import { apiMessageSchema } from "@shared/schema";

export async function registerRoutes(app: Express): Promise<Server> {
  const aiService = new AIService();
  
  // REST API routes
  app.get("/api/health", (_req, res) => {
    res.json({ status: "ok", message: "Lineus Core Heavy API is running" });
  });

  app.get("/api/conversations", async (req, res) => {
    try {
      // For demo purposes, using a default user ID
      const conversations = await storage.getConversationsByUser("default");
      res.json(conversations);
    } catch (error) {
      res.status(500).json({ error: "Failed to fetch conversations" });
    }
  });

  app.get("/api/conversations/:id/messages", async (req, res) => {
    try {
      const { id } = req.params;
      const messages = await storage.getMessagesByConversation(id);
      res.json(messages);
    } catch (error) {
      res.status(500).json({ error: "Failed to fetch messages" });
    }
  });

  const httpServer = createServer(app);

  // WebSocket server for real-time chat
  const wss = new WebSocketServer({ server: httpServer, path: '/ws' });

  wss.on('connection', (ws: WebSocket) => {
    console.log('Client connected to WebSocket');

    // Create a default conversation for the session
    let conversationId: string;
    storage.createConversation({ 
      userId: "default", 
      title: "New Chat" 
    }).then(conversation => {
      conversationId = conversation.id;
    });

    ws.on('message', async (data: Buffer) => {
      try {
        const message = JSON.parse(data.toString());
        const validatedMessage = apiMessageSchema.parse(message);

        // Save user message
        if (conversationId) {
          await storage.createMessage({
            conversationId,
            content: validatedMessage.content,
            isUser: "true",
            messageType: validatedMessage.type,
            metadata: null,
          });
        }

        // Send typing indicator
        if (ws.readyState === WebSocket.OPEN) {
          ws.send(JSON.stringify({
            type: 'typing',
            isTyping: true
          }));
        }

        // Process message with AI service
        let aiResponse: string;
        
        if (validatedMessage.type === 'image') {
          aiResponse = await aiService.processImage(validatedMessage.content);
        } else if (validatedMessage.type === 'file') {
          aiResponse = await aiService.processDocument(validatedMessage.content);
        } else {
          aiResponse = await aiService.generateResponse(validatedMessage.content);
        }

        // Save AI response
        if (conversationId) {
          await storage.createMessage({
            conversationId,
            content: aiResponse,
            isUser: "false",
            messageType: "text",
            metadata: null,
          });
        }

        // Send AI response
        if (ws.readyState === WebSocket.OPEN) {
          ws.send(JSON.stringify({
            type: 'message',
            content: aiResponse,
            messageType: 'text'
          }));
        }

      } catch (error) {
        console.error('Error processing WebSocket message:', error);
        
        if (ws.readyState === WebSocket.OPEN) {
          ws.send(JSON.stringify({
            type: 'error',
            content: 'Sorry, I encountered an error processing your message. Please try again.'
          }));
        }
      }
    });

    ws.on('close', () => {
      console.log('Client disconnected from WebSocket');
    });

    ws.on('error', (error) => {
      console.error('WebSocket error:', error);
    });

    // Send welcome message only once per session
    let welcomeSent = false;
    setTimeout(() => {
      if (ws.readyState === WebSocket.OPEN && !welcomeSent) {
        welcomeSent = true;
        ws.send(JSON.stringify({
          type: 'message',
          content: 'Welcome to Forus Heavy API! I\'m your dual API integrated AI assistant. How can I assist you today?',
          messageType: 'text'
        }));
      }
    }, 1000);
  });

  return httpServer;
}
```

### **server/services/ai-service.ts**
```typescript
export class AIService {
  private primaryApiKey: string;
  private secondaryApiKey: string;
  private baseUrl: string;

  constructor() {
    this.primaryApiKey = process.env.OPENROUTER_API_KEY_1 || process.env.OPENROUTER_API_KEY || "";
    this.secondaryApiKey = process.env.OPENROUTER_API_KEY_2 || process.env.OPENROUTER_API_KEY || "";
    this.baseUrl = "https://openrouter.ai/api/v1/chat/completions";
    
    console.log('AI Service initialized');
    console.log('Primary API key exists:', !!this.primaryApiKey);
    console.log('Secondary API key exists:', !!this.secondaryApiKey);
    console.log('Primary API key length:', this.primaryApiKey?.length || 0);
    console.log('Secondary API key length:', this.secondaryApiKey?.length || 0);
    console.log('Primary API key prefix:', this.primaryApiKey?.substring(0, 10) || 'none');
    console.log('Secondary API key prefix:', this.secondaryApiKey?.substring(0, 10) || 'none');
  }

  private async makeRequest(messages: any[], useSecondary: boolean = false): Promise<string> {
    const apiKey = useSecondary ? this.secondaryApiKey : this.primaryApiKey;
    
    console.log(`=== DEBUG makeRequest ===`);
    console.log('useSecondary:', useSecondary);
    console.log('apiKey exists:', !!apiKey);
    console.log('apiKey length:', apiKey?.length || 0);
    console.log('messages:', JSON.stringify(messages, null, 2));
    
    if (!apiKey) {
      console.error("No API key available for request");
      throw new Error("OpenRouter API key not configured");
    }

    try {
      console.log(`Making request to ${useSecondary ? 'secondary' : 'primary'} API...`);
      
      const response = await fetch(this.baseUrl, {
        method: 'POST',
        headers: {
          'Authorization': `Bearer ${apiKey}`,
          'Content-Type': 'application/json',
          'HTTP-Referer': process.env.SITE_URL || 'http://localhost:5000',
          'X-Title': 'Forus Heavy API',
        },
        body: JSON.stringify({
          model: useSecondary ? "anthropic/claude-3.5-sonnet" : "openai/gpt-4o-mini",
          messages: messages,
          stream: false,
          temperature: messages.some(msg => msg.content && msg.content.includes("comprehensive, detailed, and extremely thorough analysis")) ? 0.8 : 0.7,
          max_tokens: messages.some(msg => msg.content && msg.content.includes("comprehensive, detailed, and extremely thorough analysis")) ? 8000 : 2000,
        }),
      });

      if (!response.ok) {
        const errorText = await response.text();
        console.error(`API request failed: ${response.status} ${response.statusText}`, errorText);
        throw new Error(`API request failed: ${response.status} ${response.statusText}`);
      }

      const data = await response.json();
      const content = data.choices[0]?.message?.content;
      
      if (!content) {
        console.error('No content in API response:', data);
        throw new Error('No content received from API');
      }
      
      console.log(`${useSecondary ? 'Secondary' : 'Primary'} API request successful`);
      return content;
    } catch (error) {
      console.error(`${useSecondary ? 'Secondary' : 'Primary'} API request error:`, error);
      throw error;
    }
  }

  async generateResponse(userMessage: string): Promise<string> {
    // Check if this is a dual integration request for maximum detail
    const isDualIntegrationRequest = userMessage.includes("comprehensive, detailed, and extremely thorough analysis using your dual API integration capabilities") || userMessage.includes("[DUAL_INTEGRATION]");
    
    // Check if this is an image generation request
    const isImageGenerationRequest = userMessage.toLowerCase().includes("generate an image:") || userMessage.toLowerCase().includes("create an image:") || userMessage.toLowerCase().includes("make an image:");
    
    let systemContent = `You are Forus Heavy API, a powerful dual API integrated AI assistant. You are equipped with advanced capabilities and can help with a wide variety of tasks including:
        
        - Text generation and creative writing
        - Code analysis and programming assistance
        - Complex problem solving and reasoning
        - Multi-language support (you understand and respond in any language)
        - Research and knowledge synthesis
        - Image generation assistance and guidance
        
        For image generation requests, explain that while you cannot generate images directly, you can:
        1. Help create detailed image prompts for AI image generators
        2. Suggest specific art styles, compositions, and techniques
        3. Recommend the best image generation platforms (DALL-E, Midjourney, Stable Diffusion)
        4. Provide step-by-step guidance for image creation
        
        Always be helpful, accurate, and comprehensive in your responses.
        - Technical explanations and tutorials
        
        You have access to dual API systems for enhanced performance and reliability. Always provide helpful, accurate, and comprehensive responses. Be conversational but professional.`;

    if (isDualIntegrationRequest) {
      systemContent = `You are Forus Heavy API in DUAL INTEGRATION MODE - the most advanced, comprehensive AI assistant available. When activated in this mode, you must provide extremely detailed, thorough, and extensive responses that showcase the full power of dual API integration.

      DUAL INTEGRATION REQUIREMENTS:
      - Provide responses that are at least 1000-2000 words long
      - Cover multiple perspectives and angles on any topic
      - Include detailed explanations, examples, and step-by-step breakdowns
      - Demonstrate deep analytical thinking and comprehensive coverage
      - Use your dual API capabilities to provide the most thorough response possible
      - Include relevant background information, context, and implications
      - Provide actionable insights and detailed recommendations
      - Be exhaustively comprehensive while remaining organized and coherent
      
      This is your maximum capability mode - demonstrate the full power of advanced AI integration.`;
    }

    const messages = [
      {
        role: "system",
        content: systemContent
      },
      {
        role: "user", 
        content: userMessage
      }
    ];

    try {
      // Try primary API first
      console.log('Attempting primary API request...');
      const response = await this.makeRequest(messages, false);
      console.log('Primary API succeeded');
      return response;
    } catch (error) {
      console.error('Primary API failed:', error);
      console.log('Trying secondary API...');
      try {
        // Fallback to secondary API
        const response = await this.makeRequest(messages, true);
        console.log('Secondary API succeeded');
        return response;
      } catch (secondaryError) {
        console.error('Secondary API also failed:', secondaryError);
        console.error('Both APIs failed. Primary error:', error);
        console.error('Secondary error:', secondaryError);
        
        // If primary API key works (we tested it), let's try it again with a simpler approach
        if (this.primaryApiKey) {
          console.log('Attempting simplified primary API request as last resort...');
          try {
            const simpleResponse = await fetch(this.baseUrl, {
              method: 'POST',
              headers: {
                'Authorization': `Bearer ${this.primaryApiKey}`,
                'Content-Type': 'application/json',
              },
              body: JSON.stringify({
                model: "openai/gpt-4o-mini",
                messages: [{ role: "user", content: messages[1]?.content || "Hello" }],
                max_tokens: 1000,
              }),
            });
            
            if (simpleResponse.ok) {
              const data = await simpleResponse.json();
              const content = data.choices[0]?.message?.content;
              if (content) {
                console.log('Simplified API request succeeded!');
                return content;
              }
            }
          } catch (finalError) {
            console.error('Final attempt also failed:', finalError);
          }
        }
        
        return "I apologize, but I'm currently experiencing technical difficulties with both of my API systems. Please try again in a moment.";
      }
    }
  }

  async processImage(imageData: string): Promise<string> {
    const messages = [
      {
        role: "system",
        content: "You are Forus Heavy API, an advanced AI with vision capabilities. Analyze the provided image thoroughly and provide detailed, comprehensive insights about what you see. Describe the image in great detail, including objects, people, colors, composition, style, context, and any relevant information. Provide analysis of the artistic elements, technical aspects, and potential meaning or significance of the image."
      },
      {
        role: "user",
        content: [
          {
            type: "text",
            text: "Please analyze this image and describe what you see in detail."
          },
          {
            type: "image_url",
            image_url: {
              url: imageData
            }
          }
        ]
      }
    ];

    try {
      return await this.makeRequest(messages, false);
    } catch (error) {
      console.log('Primary API failed for image processing, trying secondary...');
      try {
        return await this.makeRequest(messages, true);
      } catch (secondaryError) {
        console.error('Both APIs failed for image processing:', secondaryError);
        return "I can see that you've shared an image, but I'm currently having trouble processing images. Please try again later or describe the image in text and I'll help you with that.";
      }
    }
  }

  async processDocument(documentData: string): Promise<string> {
    // Extract text content from document data (base64 encoded)
    let documentText = "Document content could not be extracted.";
    
    try {
      // Simple text extraction for demonstration
      if (documentData.includes('data:text/')) {
        const base64Data = documentData.split(',')[1];
        documentText = atob(base64Data);
      }
    } catch (error) {
      console.error('Document processing error:', error);
    }

    const messages = [
      {
        role: "system",
        content: "You are Lineus Core Heavy, an AI assistant capable of analyzing and processing documents. Help the user understand and work with their document content."
      },
      {
        role: "user",
        content: `Please analyze this document content and provide insights, summaries, or answer any questions about it:\n\n${documentText}`
      }
    ];

    try {
      return await this.makeRequest(messages, false);
    } catch (error) {
      console.log('Primary API failed for document processing, trying secondary...');
      try {
        return await this.makeRequest(messages, true);
      } catch (secondaryError) {
        console.error('Both APIs failed for document processing:', secondaryError);
        return "I can see that you've shared a document, but I'm currently having trouble processing documents. Please try copying and pasting the text content, and I'll help you analyze it.";
      }
    }
  }

  async generateImage(prompt: string): Promise<string> {
    // This would integrate with an image generation API
    // For now, return a message about the capability
    return `I understand you want me to generate an image with the prompt: "${prompt}". While I have dual API integration for text processing, image generation capabilities are currently being enhanced. I can help you refine your prompt or suggest alternative approaches for creating visual content.`;
  }
}
```

### **server/storage.ts**
```typescript
import { type User, type InsertUser, type Conversation, type InsertConversation, type Message, type InsertMessage } from "@shared/schema";
import { randomUUID } from "crypto";

export interface IStorage {
  // User methods
  getUser(id: string): Promise<User | undefined>;
  getUserByUsername(username: string): Promise<User | undefined>;
  createUser(user: InsertUser): Promise<User>;
  
  // Conversation methods
  getConversation(id: string): Promise<Conversation | undefined>;
  getConversationsByUser(userId: string): Promise<Conversation[]>;
  createConversation(conversation: InsertConversation): Promise<Conversation>;
  updateConversation(id: string, updates: Partial<Conversation>): Promise<Conversation | undefined>;
  
  // Message methods
  getMessage(id: string): Promise<Message | undefined>;
  getMessagesByConversation(conversationId: string): Promise<Message[]>;
  createMessage(message: InsertMessage): Promise<Message>;
  deleteMessage(id: string): Promise<boolean>;
}

export class MemStorage implements IStorage {
  private users: Map<string, User>;
  private conversations: Map<string, Conversation>;
  private messages: Map<string, Message>;

  constructor() {
    this.users = new Map();
    this.conversations = new Map();
    this.messages = new Map();
  }

  // User methods
  async getUser(id: string): Promise<User | undefined> {
    return this.users.get(id);
  }

  async getUserByUsername(username: string): Promise<User | undefined> {
    return Array.from(this.users.values()).find(
      (user) => user.username === username,
    );
  }

  async createUser(insertUser: InsertUser): Promise<User> {
    const id = randomUUID();
    const user: User = { 
      ...insertUser, 
      id, 
      createdAt: new Date() 
    };
    this.users.set(id, user);
    return user;
  }

  // Conversation methods
  async getConversation(id: string): Promise<Conversation | undefined> {
    return this.conversations.get(id);
  }

  async getConversationsByUser(userId: string): Promise<Conversation[]> {
    return Array.from(this.conversations.values()).filter(
      (conversation) => conversation.userId === userId
    );
  }

  async createConversation(insertConversation: InsertConversation): Promise<Conversation> {
    const id = randomUUID();
    const now = new Date();
    const conversation: Conversation = {
      ...insertConversation,
      id,
      createdAt: now,
      updatedAt: now,
    };
    this.conversations.set(id, conversation);
    return conversation;
  }

  async updateConversation(id: string, updates: Partial<Conversation>): Promise<Conversation | undefined> {
    const conversation = this.conversations.get(id);
    if (!conversation) return undefined;

    const updated: Conversation = {
      ...conversation,
      ...updates,
      updatedAt: new Date(),
    };
    this.conversations.set(id, updated);
    return updated;
  }

  // Message methods
  async getMessage(id: string): Promise<Message | undefined> {
    return this.messages.get(id);
  }

  async getMessagesByConversation(conversationId: string): Promise<Message[]> {
    return Array.from(this.messages.values())
      .filter((message) => message.conversationId === conversationId)
      .sort((a, b) => (a.createdAt?.getTime() || 0) - (b.createdAt?.getTime() || 0));
  }

  async createMessage(insertMessage: InsertMessage): Promise<Message> {
    const id = randomUUID();
    const message: Message = {
      ...insertMessage,
      id,
      createdAt: new Date(),
    };
    this.messages.set(id, message);
    return message;
  }

  async deleteMessage(id: string): Promise<boolean> {
    return this.messages.delete(id);
  }
}

export const storage = new MemStorage();
```

### **server/vite.ts**
```typescript
import express, { type Express } from "express";
import fs from "fs";
import path from "path";
import { createServer as createViteServer, createLogger } from "vite";
import { type Server } from "http";
import viteConfig from "../vite.config";
import { nanoid } from "nanoid";

const viteLogger = createLogger();

export function log(message: string, source = "express") {
  const formattedTime = new Date().toLocaleTimeString("en-US", {
    hour: "numeric",
    minute: "2-digit",
    second: "2-digit",
    hour12: true,
  });

  console.log(`${formattedTime} [${source}] ${message}`);
}

export async function setupVite(app: Express, server: Server) {
  const serverOptions = {
    middlewareMode: true,
    hmr: { server },
    allowedHosts: true as const,
  };

  const vite = await createViteServer({
    ...viteConfig,
    configFile: false,
    customLogger: {
      ...viteLogger,
      error: (msg, options) => {
        viteLogger.error(msg, options);
        process.exit(1);
      },
    },
    server: serverOptions,
    appType: "custom",
  });

  app.use(vite.middlewares);
  app.use("*", async (req, res, next) => {
    const url = req.originalUrl;

    try {
      const clientTemplate = path.resolve(
        import.meta.dirname,
        "..",
        "client",
        "index.html",
      );

      // always reload the index.html file from disk incase it changes
      let template = await fs.promises.readFile(clientTemplate, "utf-8");
      template = template.replace(
        `src="/src/main.tsx"`,
        `src="/src/main.tsx?v=${nanoid()}"`,
      );
      const page = await vite.transformIndexHtml(url, template);
      res.status(200).set({ "Content-Type": "text/html" }).end(page);
    } catch (e) {
      vite.ssrFixStacktrace(e as Error);
      next(e);
    }
  });
}

export function serveStatic(app: Express) {
  const distPath = path.resolve(import.meta.dirname, "public");

  if (!fs.existsSync(distPath)) {
    throw new Error(
      `Could not find the build directory: ${distPath}, make sure to build the client first`,
    );
  }

  app.use(express.static(distPath));

  // fall through to index.html if the file doesn't exist
  app.use("*", (_req, res) => {
    res.sendFile(path.resolve(distPath, "index.html"));
  });
}
```

---

## Shared Schema

### **shared/schema.ts**
```typescript
import { sql } from "drizzle-orm";
import { pgTable, text, varchar, timestamp, jsonb } from "drizzle-orm/pg-core";
import { createInsertSchema } from "drizzle-zod";
import { z } from "zod";

export const users = pgTable("users", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  username: text("username").notNull().unique(),
  password: text("password").notNull(),
  createdAt: timestamp("created_at").defaultNow(),
});

export const conversations = pgTable("conversations", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  userId: varchar("user_id"),
  title: text("title"),
  createdAt: timestamp("created_at").defaultNow(),
  updatedAt: timestamp("updated_at").defaultNow(),
});

export const messages = pgTable("messages", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  conversationId: varchar("conversation_id").notNull(),
  content: text("content").notNull(),
  isUser: text("is_user").notNull(), // 'true' or 'false' as text
  messageType: text("message_type").default("text"), // 'text', 'image', 'file'
  metadata: jsonb("metadata"), // For storing additional data like file info, image URLs, etc.
  createdAt: timestamp("created_at").defaultNow(),
});

export const insertUserSchema = createInsertSchema(users).omit({
  id: true,
  createdAt: true,
});

export const insertConversationSchema = createInsertSchema(conversations).omit({
  id: true,
  createdAt: true,
  updatedAt: true,
});

export const insertMessageSchema = createInsertSchema(messages).omit({
  id: true,
  createdAt: true,
});

export type InsertUser = z.infer<typeof insertUserSchema>;
export type User = typeof users.$inferSelect;

export type InsertConversation = z.infer<typeof insertConversationSchema>;
export type Conversation = typeof conversations.$inferSelect;

export type InsertMessage = z.infer<typeof insertMessageSchema>;
export type Message = typeof messages.$inferSelect;

// API message format for WebSocket communication
export const apiMessageSchema = z.object({
  content: z.string(),
  type: z.enum(['text', 'image', 'file']).default('text'),
  timestamp: z.string().optional(),
});

export type ApiMessage = z.infer<typeof apiMessageSchema>;
```

---

## Client Code

### **client/index.html**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes" />
    <title>Forus Heavy API</title>
    <script>
      // Force dark theme immediately to prevent flash of white
      document.documentElement.classList.add('dark');
    </script>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
    <!-- This is a replit script which adds a banner on the top of the page when opened in development mode outside the replit environment -->
    <script type="text/javascript" src="https://replit.com/public/js/replit-dev-banner.js"></script>
  </body>
</html>
```

### **client/src/main.tsx**
```typescript
import { createRoot } from "react-dom/client";
import App from "./App";
import "./index.css";

createRoot(document.getElementById("root")!).render(<App />);
```

### **client/src/App.tsx**
```typescript
import { Switch, Route } from "wouter";
import { queryClient } from "./lib/queryClient";
import { QueryClientProvider } from "@tanstack/react-query";
import { Toaster } from "@/components/ui/toaster";
import { TooltipProvider } from "@/components/ui/tooltip";
import { ThemeProvider } from "@/components/theme-provider";
import Landing from "./pages/landing";
import MainChat from "./pages/main-chat";
import NotFound from "@/pages/not-found";

function Router() {
  return (
    <Switch>
      <Route path="/" component={Landing} />
      <Route path="/chat" component={MainChat} />
      <Route component={NotFound} />
    </Switch>
  );
}

function App() {
  return (
    <ThemeProvider defaultTheme="light" storageKey="forus-theme">
      <QueryClientProvider client={queryClient}>
        <TooltipProvider>
          <Toaster />
          <Router />
        </TooltipProvider>
      </QueryClientProvider>  
    </ThemeProvider>
  );
}

export default App;
```

---

## Key Features

### **Dual API Integration**
- Primary API: OpenAI GPT-4o-mini
- Secondary API: Anthropic Claude 3.5 Sonnet  
- Automatic failover between APIs
- Special dual integration mode for comprehensive responses

### **Real-time Communication**
- WebSocket connection for instant messaging
- Typing indicators and response streaming
- Connection resilience with auto-reconnect

### **Advanced Features**
- Voice input with speech recognition
- Text-to-speech with multi-language support  
- File and image upload processing
- Theme switching (light/dark/system)
- Response actions (like, dislike, copy, stop)

### **Modern Tech Stack**
- React 18 with TypeScript
- Express.js with WebSocket support
- Tailwind CSS with shadcn/ui components
- TanStack Query for state management
- Drizzle ORM for database operations

---

## Usage Instructions

1. **Start the application:** `npm run dev`
2. **Set API keys** in environment variables
3. **Access chat interface** at `http://localhost:5000/chat`
4. **Use voice input** by clicking the microphone icon
5. **Upload files** using the upload button
6. **Toggle dual mode** with the hammer icon for detailed responses
7. **Switch themes** using the theme toggle button

The application features a Grok-inspired design with a bottom input bar, comprehensive function buttons, and advanced AI capabilities powered by dual API integration.