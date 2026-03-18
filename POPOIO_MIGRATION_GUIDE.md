# Popoio - Guía Completa de Migración

## Instrucciones de Setup

### 1. Crear el proyecto
```bash
mkdir popoio && cd popoio
npm init -y
```

### 2. Instalar dependencias
```bash
npm install @hookform/resolvers @neondatabase/serverless @radix-ui/react-accordion @radix-ui/react-dialog @radix-ui/react-label @radix-ui/react-slot @radix-ui/react-toast @radix-ui/react-tooltip @tanstack/react-query class-variance-authority clsx date-fns dompurify drizzle-orm drizzle-zod express isomorphic-dompurify lucide-react react react-dom react-hook-form resend sonner tailwind-merge tw-animate-css wouter ws zod zod-validation-error

npm install -D @tailwindcss/vite @types/dompurify @types/express @types/node @types/react @types/react-dom @types/ws @vitejs/plugin-react autoprefixer drizzle-kit esbuild postcss tailwindcss tsx typescript vite
```

### 3. Variables de entorno necesarias (.env)
```
DATABASE_URL=postgresql://user:password@host:5432/dbname
RESEND_API_KEY=tu_clave_de_resend
PORT=5000
```

### 4. Crear la base de datos
```bash
npx drizzle-kit push
```

### 5. Ejecutar el seed (datos iniciales)
```bash
npx tsx server/seed.ts
```

### 6. Arrancar el proyecto
```bash
npm run dev
```

### 7. Assets de video/imagen
Los videos están en `attached_assets/generated_videos/` y el logo en `attached_assets/Popoio - Logo_1763637341361.png`. Deberás copiar estos archivos manualmente al mismo directorio en tu proyecto nuevo.

---

## Estructura de archivos

```
popoio/
├── package.json
├── tsconfig.json
├── vite.config.ts
├── drizzle.config.ts
├── postcss.config.js
├── components.json
├── attached_assets/
│   ├── Popoio - Logo_1763637341361.png
│   └── generated_videos/
│       ├── abstract_medical_technology_waves_in_teal_and_cream.mp4
│       ├── cinematic_pan_of_a_modern_dental_clinic_reception.mp4
│       ├── clean_patient_list_scrolling_on_tablet.mp4
│       ├── doctor_using_futuristic_tablet_interface.mp4
│       ├── futuristic_medical_dashboard_interface_with_teal_glow.mp4
│       └── smartphone_receiving_medical_appointment_notification.mp4
├── shared/
│   └── schema.ts
├── db/
│   └── index.ts
├── server/
│   ├── index.ts
│   ├── routes.ts
│   ├── storage.ts
│   ├── seed.ts
│   └── vite.ts
└── client/
    ├── index.html
    └── src/
        ├── main.tsx
        ├── App.tsx
        ├── index.css
        ├── lib/
        │   ├── queryClient.ts
        │   └── utils.ts
        ├── hooks/
        │   ├── use-toast.ts
        │   └── use-mobile.tsx
        ├── pages/
        │   ├── home.tsx
        │   ├── blog.tsx
        │   ├── blog-article.tsx
        │   ├── faq.tsx
        │   ├── dashboard.tsx
        │   ├── login.tsx
        │   └── not-found.tsx
        └── components/
            ├── contact-form-dialog.tsx
            └── ui/
                ├── accordion.tsx
                ├── button.tsx
                ├── card.tsx
                ├── dialog.tsx
                ├── footer.tsx
                ├── form.tsx
                ├── input.tsx
                ├── label.tsx
                ├── navbar.tsx
                ├── toast.tsx
                ├── toaster.tsx
                └── tooltip.tsx
```

---

## ARCHIVOS DEL PROYECTO

---

### `package.json`
```json
{
  "name": "rest-express",
  "version": "1.0.0",
  "type": "module",
  "license": "MIT",
  "scripts": {
    "dev:client": "vite dev --port 5000",
    "dev": "NODE_ENV=development tsx server/index.ts",
    "build": "vite build && esbuild server/index.ts --platform=node --packages=external --bundle --format=esm --outdir=dist",
    "start": "NODE_ENV=production node dist/index.js",
    "check": "tsc",
    "db:push": "drizzle-kit push"
  },
  "dependencies": {
    "@hookform/resolvers": "^3.10.0",
    "@neondatabase/serverless": "^0.10.4",
    "@radix-ui/react-accordion": "^1.2.12",
    "@radix-ui/react-dialog": "^1.1.15",
    "@radix-ui/react-label": "^2.1.8",
    "@radix-ui/react-slot": "^1.2.4",
    "@radix-ui/react-toast": "^1.2.7",
    "@radix-ui/react-tooltip": "^1.2.8",
    "@tanstack/react-query": "^5.60.5",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "date-fns": "^3.6.0",
    "dompurify": "^3.3.0",
    "drizzle-orm": "^0.39.1",
    "drizzle-zod": "^0.7.0",
    "express": "^4.21.2",
    "isomorphic-dompurify": "^2.30.0",
    "lucide-react": "^0.545.0",
    "react": "^19.2.0",
    "react-dom": "^19.2.0",
    "react-hook-form": "^7.66.0",
    "resend": "^6.5.2",
    "sonner": "^2.0.7",
    "tailwind-merge": "^3.3.1",
    "tw-animate-css": "^1.4.0",
    "wouter": "^3.3.5",
    "ws": "^8.18.0",
    "zod": "^3.25.76",
    "zod-validation-error": "^3.4.0"
  },
  "devDependencies": {
    "@tailwindcss/vite": "^4.1.14",
    "@types/dompurify": "^3.0.5",
    "@types/express": "4.17.21",
    "@types/node": "^20.19.0",
    "@types/react": "^19.2.0",
    "@types/react-dom": "^19.2.0",
    "@types/ws": "^8.5.13",
    "@vitejs/plugin-react": "^5.0.4",
    "autoprefixer": "^10.4.21",
    "drizzle-kit": "^0.31.4",
    "esbuild": "^0.25.0",
    "postcss": "^8.5.6",
    "tailwindcss": "^4.1.14",
    "tsx": "^4.20.5",
    "typescript": "5.6.3",
    "vite": "^7.1.9"
  },
  "optionalDependencies": {
    "bufferutil": "^4.0.8"
  }
}
```

---

### `tsconfig.json`
```json
{
  "include": ["client/src/**/*", "shared/**/*", "server/**/*"],
  "exclude": ["node_modules", "build", "dist", "**/*.test.ts"],
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./node_modules/typescript/tsbuildinfo",
    "noEmit": true,
    "module": "ESNext",
    "strict": true,
    "lib": ["esnext", "dom", "dom.iterable"],
    "jsx": "preserve",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "allowImportingTsExtensions": true,
    "moduleResolution": "bundler",
    "baseUrl": ".",
    "types": ["node", "vite/client"],
    "paths": {
      "@/*": ["./client/src/*"],
      "@shared/*": ["./shared/*"]
    }
  }
}
```

---

### `vite.config.ts`
```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";
import path from "path";

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
  resolve: {
    alias: {
      "@": path.resolve(import.meta.dirname, "client", "src"),
      "@shared": path.resolve(import.meta.dirname, "shared"),
      "@assets": path.resolve(import.meta.dirname, "attached_assets"),
    },
  },
  css: {
    postcss: {
      plugins: [],
    },
  },
  root: path.resolve(import.meta.dirname, "client"),
  build: {
    outDir: path.resolve(import.meta.dirname, "dist/public"),
    emptyOutDir: true,
  },
  server: {
    host: "0.0.0.0",
    allowedHosts: true,
    fs: {
      strict: true,
      deny: ["**/.*"],
    },
  },
});
```

---

### `drizzle.config.ts`
```ts
import { defineConfig } from "drizzle-kit";

if (!process.env.DATABASE_URL) {
  throw new Error("DATABASE_URL, ensure the database is provisioned");
}

export default defineConfig({
  out: "./migrations",
  schema: "./shared/schema.ts",
  dialect: "postgresql",
  dbCredentials: {
    url: process.env.DATABASE_URL,
  },
});
```

---

### `postcss.config.js`
```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

### `components.json`
```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": false,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "client/src/index.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "iconLibrary": "lucide",
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  }
}
```

---

### `shared/schema.ts`
```ts
import { sql } from "drizzle-orm";
import { pgTable, text, varchar, serial, timestamp, integer } from "drizzle-orm/pg-core";
import { createInsertSchema } from "drizzle-zod";
import { z } from "zod";

export const users = pgTable("users", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  username: text("username").notNull().unique(),
  password: text("password").notNull(),
});

export const insertUserSchema = createInsertSchema(users).pick({
  username: true,
  password: true,
});

export type InsertUser = z.infer<typeof insertUserSchema>;
export type User = typeof users.$inferSelect;

export const contactSubmissions = pgTable("contact_submissions", {
  id: serial("id").primaryKey(),
  name: text("name").notNull(),
  email: text("email").notNull(),
  phone: text("phone"),
  createdAt: timestamp("created_at").defaultNow().notNull(),
});

export const insertContactSubmissionSchema = createInsertSchema(contactSubmissions).omit({
  id: true,
  createdAt: true,
});

export type InsertContactSubmission = z.infer<typeof insertContactSubmissionSchema>;
export type ContactSubmission = typeof contactSubmissions.$inferSelect;

export const blogArticles = pgTable("blog_articles", {
  id: serial("id").primaryKey(),
  slug: text("slug").notNull().unique(),
  title: text("title").notNull(),
  metaDescription: text("meta_description").notNull(),
  metaKeywords: text("meta_keywords"),
  excerpt: text("excerpt").notNull(),
  content: text("content").notNull(),
  coverImage: text("cover_image"),
  author: text("author").notNull(),
  publishedAt: timestamp("published_at").defaultNow().notNull(),
  updatedAt: timestamp("updated_at").defaultNow().notNull(),
  tags: text("tags").array(),
});

export const insertBlogArticleSchema = createInsertSchema(blogArticles).omit({
  id: true,
});

export type InsertBlogArticle = z.infer<typeof insertBlogArticleSchema>;
export type BlogArticle = typeof blogArticles.$inferSelect;

export const faqs = pgTable("faqs", {
  id: serial("id").primaryKey(),
  question: text("question").notNull(),
  answer: text("answer").notNull(),
  category: text("category").notNull(),
  order: integer("order").notNull().default(0),
  createdAt: timestamp("created_at").defaultNow().notNull(),
});

export const insertFaqSchema = createInsertSchema(faqs).omit({
  id: true,
  createdAt: true,
});

export type InsertFaq = z.infer<typeof insertFaqSchema>;
export type Faq = typeof faqs.$inferSelect;
```

---

### `db/index.ts`
```ts
import { drizzle } from "drizzle-orm/neon-serverless";
import ws from "ws";
import * as schema from "@shared/schema";

if (!process.env.DATABASE_URL) {
  throw new Error(
    "DATABASE_URL must be set. Did you forget to provision a database?",
  );
}

export const db = drizzle({
  connection: process.env.DATABASE_URL,
  schema,
  ws: ws,
});
```

---

### `server/index.ts`
```ts
import express, { type Request, Response, NextFunction } from "express";
import { registerRoutes } from "./routes";
import { setupVite, serveStatic, log } from "./vite";

const app = express();

declare module 'http' {
  interface IncomingMessage {
    rawBody: unknown
  }
}
app.use(express.json({
  verify: (req, _res, buf) => {
    req.rawBody = buf;
  }
}));
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

  if (app.get("env") === "development") {
    await setupVite(app, server);
  } else {
    serveStatic(app);
  }

  const port = parseInt(process.env.PORT || '5000', 10);
  server.listen({
    port,
    host: "0.0.0.0",
    reusePort: true,
  }, () => {
    log(`serving on port ${port}`);
  });
})();
```

---

### `server/routes.ts`
```ts
import type { Express } from "express";
import { createServer, type Server } from "http";
import { storage } from "./storage";
import { insertContactSubmissionSchema } from "@shared/schema";
import { z } from "zod";
import { Resend } from "resend";

const resend = new Resend(process.env.RESEND_API_KEY);

export async function registerRoutes(app: Express): Promise<Server> {
  app.post("/api/contact", async (req, res) => {
    try {
      const validatedData = insertContactSubmissionSchema.parse(req.body);
      const submission = await storage.createContactSubmission(validatedData);
      
      console.log("New contact submission:", {
        name: submission.name,
        email: submission.email,
        phone: submission.phone,
        timestamp: submission.createdAt
      });

      try {
        console.log("Intentando enviar email via Resend...");
        const emailResponse = await resend.emails.send({
          from: 'Popoio <noreply@popoio.com>',
          to: ['diogo@468cap.com', 'diogococunha@gmail.com'],
          subject: `Nuevo Lead: ${submission.name}`,
          html: `
            <div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
              <h2 style="color: #176060;">Nuevo contacto desde Popoio.com</h2>
              <div style="background-color: #f5f5f5; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <p><strong>Nombre:</strong> ${submission.name}</p>
                <p><strong>Email:</strong> <a href="mailto:${submission.email}">${submission.email}</a></p>
                ${submission.phone ? `<p><strong>Telefono:</strong> ${submission.phone}</p>` : ''}
                <p style="color: #666; font-size: 12px;">Recibido: ${new Date(submission.createdAt).toLocaleString('es-ES')}</p>
              </div>
            </div>
          `,
        });
        console.log("Respuesta de Resend:", JSON.stringify(emailResponse, null, 2));
      } catch (emailError) {
        console.error("Error al enviar email:", emailError);
      }

      res.json({ 
        success: true, 
        message: "Formulario enviado correctamente. Te contactaremos pronto."
      });
    } catch (error) {
      if (error instanceof z.ZodError) {
        res.status(400).json({ success: false, message: "Datos invalidos", errors: error.errors });
      } else {
        console.error("Error saving contact submission:", error);
        res.status(500).json({ success: false, message: "Error al procesar el formulario" });
      }
    }
  });

  app.get("/api/contacts", async (req, res) => {
    try {
      const contacts = await storage.getAllContactSubmissions();
      res.json(contacts);
    } catch (error) {
      console.error("Error fetching contacts:", error);
      res.status(500).json({ success: false, message: "Error al obtener contactos" });
    }
  });

  app.get("/api/blog", async (req, res) => {
    try {
      const articles = await storage.getAllBlogArticles();
      res.json(articles);
    } catch (error) {
      console.error("Error fetching blog articles:", error);
      res.status(500).json({ success: false, message: "Error al obtener articulos" });
    }
  });

  app.get("/api/blog/:slug", async (req, res) => {
    try {
      const article = await storage.getBlogArticleBySlug(req.params.slug);
      if (!article) {
        res.status(404).json({ success: false, message: "Articulo no encontrado" });
        return;
      }
      res.json(article);
    } catch (error) {
      console.error("Error fetching blog article:", error);
      res.status(500).json({ success: false, message: "Error al obtener articulo" });
    }
  });

  app.get("/api/faqs", async (req, res) => {
    try {
      const faqList = await storage.getAllFaqs();
      res.json(faqList);
    } catch (error) {
      console.error("Error fetching FAQs:", error);
      res.status(500).json({ success: false, message: "Error al obtener FAQs" });
    }
  });

  const httpServer = createServer(app);

  return httpServer;
}
```

---

### `server/storage.ts`
```ts
import { db } from "../db";
import { type User, type InsertUser, type ContactSubmission, type InsertContactSubmission, type BlogArticle, type InsertBlogArticle, type Faq, type InsertFaq, users, contactSubmissions, blogArticles, faqs } from "@shared/schema";
import { eq, desc } from "drizzle-orm";

export interface IStorage {
  getUser(id: string): Promise<User | undefined>;
  getUserByUsername(username: string): Promise<User | undefined>;
  createUser(user: InsertUser): Promise<User>;
  createContactSubmission(contact: InsertContactSubmission): Promise<ContactSubmission>;
  getAllContactSubmissions(): Promise<ContactSubmission[]>;
  getAllBlogArticles(): Promise<BlogArticle[]>;
  getBlogArticleBySlug(slug: string): Promise<BlogArticle | undefined>;
  createBlogArticle(article: InsertBlogArticle): Promise<BlogArticle>;
  getAllFaqs(): Promise<Faq[]>;
  createFaq(faq: InsertFaq): Promise<Faq>;
}

export class DatabaseStorage implements IStorage {
  async getUser(id: string): Promise<User | undefined> {
    const result = await db.select().from(users).where(eq(users.id, id)).limit(1);
    return result[0];
  }

  async getUserByUsername(username: string): Promise<User | undefined> {
    const result = await db.select().from(users).where(eq(users.username, username)).limit(1);
    return result[0];
  }

  async createUser(insertUser: InsertUser): Promise<User> {
    const result = await db.insert(users).values(insertUser).returning();
    return result[0];
  }

  async createContactSubmission(contact: InsertContactSubmission): Promise<ContactSubmission> {
    const result = await db.insert(contactSubmissions).values(contact).returning();
    return result[0];
  }

  async getAllContactSubmissions(): Promise<ContactSubmission[]> {
    return db.select().from(contactSubmissions).orderBy(contactSubmissions.createdAt);
  }

  async getAllBlogArticles(): Promise<BlogArticle[]> {
    return db.select().from(blogArticles).orderBy(desc(blogArticles.publishedAt));
  }

  async getBlogArticleBySlug(slug: string): Promise<BlogArticle | undefined> {
    const result = await db.select().from(blogArticles).where(eq(blogArticles.slug, slug)).limit(1);
    return result[0];
  }

  async createBlogArticle(article: InsertBlogArticle): Promise<BlogArticle> {
    const result = await db.insert(blogArticles).values(article).returning();
    return result[0];
  }

  async getAllFaqs(): Promise<Faq[]> {
    return db.select().from(faqs).orderBy(faqs.order, faqs.id);
  }

  async createFaq(faq: InsertFaq): Promise<Faq> {
    const result = await db.insert(faqs).values(faq).returning();
    return result[0];
  }
}

export const storage = new DatabaseStorage();
```

---

### `server/vite.ts`
```ts
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

  app.use("*", (_req, res) => {
    res.sendFile(path.resolve(distPath, "index.html"));
  });
}
```

---

### `server/seed.ts`
```ts
import { storage } from "./storage";
import type { InsertBlogArticle, InsertFaq } from "@shared/schema";

const blogArticles: InsertBlogArticle[] = [
  {
    slug: "transformacion-digital-clinicas-medicas-espana",
    title: "Transformacion Digital en Clinicas Medicas: Guia Completa 2025",
    metaDescription: "Descubre como la transformacion digital esta revolucionando las clinicas medicas en Espana. Guia practica con casos de exito, herramientas y estrategias probadas.",
    metaKeywords: "transformacion digital clinicas, software medico Espana, digitalizacion clinicas, tecnologia sanitaria",
    excerpt: "La transformacion digital ya no es opcional para las clinicas medicas. Descubre como adoptar tecnologia de vanguardia puede aumentar tu eficiencia hasta un 45% y mejorar la experiencia del paciente.",
    content: `
      <article class="prose max-w-none">
        <h2>El Futuro de la Gestion Clinica Llego</h2>
        
        <p>En 2025, las clinicas medicas en Espana enfrentan un punto de inflexion critico. La transformacion digital ha pasado de ser una ventaja competitiva a convertirse en una necesidad absoluta para la supervivencia y crecimiento de cualquier practica medica.</p>

        <h3>Por Que Ahora?</h3>
        
        <p>Los pacientes modernos esperan la misma experiencia digital que reciben en otros sectores. Reservas online, recordatorios automaticos, acceso a historiales medicos y comunicacion fluida ya no son lujos, son estandares.</p>

        <div class="bg-teal-50 p-6 rounded-lg my-8">
          <h4 class="text-teal-900 font-bold">Datos Clave del Sector</h4>
          <ul>
            <li>73% de los pacientes prefieren clinicas con sistemas de reserva online</li>
            <li>Las clinicas digitalizadas reducen el no-show en un 25%</li>
            <li>El tiempo administrativo disminuye hasta 3 horas diarias</li>
            <li>La satisfaccion del paciente aumenta un 40% con sistemas modernos</li>
          </ul>
        </div>

        <h3>Los 5 Pilares de la Transformacion Digital</h3>

        <h4>1. Sistema de Gestion Inteligente</h4>
        <p>Un CRM medico moderno centraliza toda la informacion del paciente: historial, citas, tratamientos, pagos y comunicaciones. La clave esta en la facilidad de uso. Si tu equipo necesita mas de una tarde para aprender el sistema, es demasiado complejo.</p>

        <h4>2. Automatizacion de Comunicaciones</h4>
        <p>Los recordatorios automaticos por WhatsApp y email son fundamentales. Cada cita perdida representa una perdida media de 150-300EUR. Un sistema que reduzca el no-show en un 25% puede generar hasta 30.000EUR adicionales anuales en una clinica mediana.</p>

        <h4>3. Paneles de Control en Tiempo Real</h4>
        <p>Los mejores directores medicos toman decisiones basadas en datos, no en intuiciones. Un dashboard visual te muestra instantaneamente: ocupacion de agenda, ingresos por servicio, pacientes nuevos vs recurrentes, y tendencias mensuales.</p>

        <h4>4. Experiencia del Paciente</h4>
        <p>La tecnologia debe mejorar, no complicar. Sistemas de check-in digital, formularios pre-consulta online y acceso a resultados reducen el tiempo de espera y mejoran la satisfaccion del paciente significativamente.</p>

        <h4>5. Seguridad y Cumplimiento RGPD</h4>
        <p>La proteccion de datos medicos es critica. Tu sistema debe cumplir con el RGPD europeo, incluir cifrado de extremo a extremo y generar logs de auditoria automaticos.</p>

        <h3>Casos de Exito Reales</h3>

        <blockquote class="border-l-4 border-teal-600 pl-6 italic my-8">
          "Antes dedicabamos 4 horas diarias a tareas administrativas. Con Popoio, se redujo a menos de 1 hora. Ahora podemos atender 6 pacientes mas al dia."
          <footer class="text-sm text-gray-600 mt-2">- Dra. Leire Boccio, Clinica Dental Barcelona</footer>
        </blockquote>

        <h3>Implementacion: El Plan de 30 Dias</h3>

        <p><strong>Semana 1:</strong> Migracion de datos y configuracion inicial<br/>
        <strong>Semana 2:</strong> Formacion del equipo (1-2 sesiones de 2 horas)<br/>
        <strong>Semana 3:</strong> Periodo de prueba con doble sistema<br/>
        <strong>Semana 4:</strong> Transicion completa y optimizacion</p>

        <h3>ROI Esperado</h3>

        <p>Una inversion de 600EUR/mes en digitalizacion genera tipicamente:</p>
        <ul>
          <li>Ahorro de 120 horas mensuales de trabajo administrativo (valor: ~2.400EUR)</li>
          <li>Reduccion del 25% en no-shows (valor: ~2.000-5.000EUR/mes)</li>
          <li>Aumento del 15% en conversion de primeras visitas (valor: variable)</li>
          <li>ROI total estimado: 300-500% en el primer ano</li>
        </ul>

        <h3>Conclusion</h3>

        <p>La transformacion digital no es un gasto, es la mejor inversion que puede hacer una clinica moderna. La pregunta no es "debo digitalizarme?" sino "cuanto estoy perdiendo cada mes que no lo hago?"</p>

        <p>Las clinicas que adoptan tecnologia de vanguardia hoy seran las lideres del mercado manana. Las que esperan, arriesgan quedarse atras en un sector cada vez mas competitivo.</p>
      </article>
    `,
    coverImage: null,
    author: "Dr. Carlos Mendoza",
    publishedAt: new Date("2025-01-15"),
    updatedAt: new Date("2025-01-15"),
    tags: ["transformacion digital", "gestion clinica", "tecnologia medica", "software sanitario"],
  },
  {
    slug: "reducir-no-show-pacientes-clinica-dental",
    title: "Como Reducir el No-Show en tu Clinica Dental: 7 Estrategias Probadas",
    metaDescription: "Reduce hasta un 60% el no-show en tu clinica dental con estas estrategias probadas. Recordatorios automaticos, confirmaciones y tecnicas de engagement de pacientes.",
    metaKeywords: "no-show clinica dental, pacientes que no acuden, recordatorios automaticos, gestion de citas dentales",
    excerpt: "El no-show de pacientes puede costar a una clinica dental entre 20.000EUR y 60.000EUR anuales. Descubre las 7 estrategias que han reducido el absentismo hasta un 60% en clinicas lideres.",
    content: `
      <article class="prose max-w-none">
        <h2>El Problema Silencioso que Afecta tu Rentabilidad</h2>
        
        <p>Una agenda con huecos es dinero perdido. Cada cita cancelada sin previo aviso representa no solo los ingresos de esa sesion, sino tambien el coste de oportunidad de haber reservado ese espacio para otro paciente.</p>

        <div class="bg-red-50 p-6 rounded-lg my-8">
          <h4 class="text-red-900 font-bold">El Coste Real del No-Show</h4>
          <p>Una clinica dental promedio con:</p>
          <ul>
            <li>30 citas semanales</li>
            <li>20% de tasa de no-show (6 citas perdidas)</li>
            <li>Ticket medio de 120EUR</li>
          </ul>
          <p class="font-bold text-xl text-red-700 mt-4">= 37.440EUR anuales perdidos</p>
        </div>

        <h3>Las 7 Estrategias Mas Efectivas</h3>

        <h4>1. Sistema de Triple Recordatorio</h4>
        <p>La tecnica mas efectiva segun estudios europeos:</p>
        <ul>
          <li><strong>7 dias antes:</strong> Email de confirmacion</li>
          <li><strong>48 horas antes:</strong> WhatsApp con boton de confirmacion</li>
          <li><strong>24 horas antes:</strong> SMS de recordatorio final</li>
        </ul>
        <p><strong>Resultado:</strong> Reduccion del 40% en no-show</p>

        <h4>2. Confirmacion Obligatoria</h4>
        <p>Implementa un sistema donde los pacientes deben confirmar activamente su cita 48 horas antes. Los pacientes que confirman tienen un 85% mas de probabilidad de asistir.</p>

        <h4>3. Lista de Espera Inteligente</h4>
        <p>Cuando un paciente cancela, un sistema automatizado notifica inmediatamente a pacientes en lista de espera. Esto permite rellenar huecos en menos de 2 horas en el 60% de los casos.</p>

        <h4>4. Politica de Cancelacion Clara</h4>
        <p>Comunica claramente:</p>
        <ul>
          <li>Se requiere cancelacion con 24 horas de antelacion</li>
          <li>Tras 2 no-shows, se requerira un deposito para futuras citas</li>
          <li>Los pacientes que cancelan con 48h de antelacion reciben prioridad en reprogramacion</li>
        </ul>

        <h4>5. Gamificacion de la Puntualidad</h4>
        <p>Implementa un sistema de "puntos de fidelidad" donde la asistencia puntual se recompensa con descuentos en tratamientos futuros. Clinicas que lo implementan reportan un 30% de mejora en asistencia.</p>

        <h4>6. Horarios Estrategicos</h4>
        <p>Analisis de datos revela que las citas programadas a estas horas tienen menor no-show:</p>
        <ul>
          <li>Martes y miercoles (menor tasa de cancelacion)</li>
          <li>10:00-11:00 y 16:00-17:00 (horas con mejor asistencia)</li>
          <li>Evitar primeras horas del lunes (30% mas de no-show)</li>
        </ul>

        <h4>7. Comunicacion Personalizada</h4>
        <p>Los mensajes genericos tienen menos impacto. Personaliza con:</p>
        <ul>
          <li>Nombre del paciente y del doctor</li>
          <li>Tipo de tratamiento especifico</li>
          <li>Recordatorio de la importancia del tratamiento</li>
        </ul>

        <h3>Tecnologia: El Multiplicador de Resultados</h3>

        <p>Implementar estas estrategias manualmente es imposible. Necesitas un sistema que automatice:</p>
        <ul>
          <li>Envio de recordatorios multicanal</li>
          <li>Gestion de confirmaciones</li>
          <li>Alertas de lista de espera</li>
          <li>Analytics de patrones de no-show</li>
        </ul>

        <blockquote class="border-l-4 border-teal-600 pl-6 italic my-8">
          "Antes teniamos 8-10 huecos semanales por no-show. Con el sistema automatizado, bajamos a 2-3. El ROI fue positivo desde el primer mes."
          <footer class="text-sm text-gray-600 mt-2">- Dr. Marcos Ruiz, Clinica Dental Valencia</footer>
        </blockquote>

        <h3>Metricas de Exito</h3>

        <p>Mide estos KPIs mensualmente:</p>
        <ul>
          <li><strong>Tasa de no-show:</strong> Objetivo menor a 10%</li>
          <li><strong>Tasa de confirmacion:</strong> Objetivo mayor a 80%</li>
          <li><strong>Tiempo promedio de rellenado de huecos:</strong> Objetivo menor a 4 horas</li>
          <li><strong>Tasa de reprogramacion:</strong> Objetivo mayor a 70%</li>
        </ul>

        <h3>Plan de Accion Inmediato</h3>

        <p><strong>Esta semana:</strong></p>
        <ol>
          <li>Calcula tu tasa actual de no-show y su coste anual</li>
          <li>Implementa recordatorios automaticos por WhatsApp</li>
          <li>Establece una politica clara de cancelacion</li>
        </ol>

        <p><strong>Este mes:</strong></p>
        <ol>
          <li>Integra un sistema de confirmacion obligatoria</li>
          <li>Crea una lista de espera automatizada</li>
          <li>Analiza patrones de no-show por dia/hora</li>
        </ol>

        <h3>Conclusion</h3>

        <p>Reducir el no-show no es cuestion de suerte, es cuestion de sistema. Las clinicas que implementan estas 7 estrategias de forma consistente logran tasas de asistencia superiores al 92%, transformando cada semana potencialmente perdida en semanas llenas y rentables.</p>

        <p>La pregunta es: Cuanto dinero estas dejando sobre la mesa este mes?</p>
      </article>
    `,
    coverImage: null,
    author: "Dra. Ana Martinez",
    publishedAt: new Date("2025-02-01"),
    updatedAt: new Date("2025-02-01"),
    tags: ["no-show", "clinica dental", "gestion de citas", "recordatorios automaticos", "whatsapp"],
  },
  {
    slug: "crm-medico-vs-excel-cual-elegir",
    title: "CRM Medico vs Excel: Analisis Completo para Clinicas en 2025",
    metaDescription: "Comparativa detallada entre CRM medico y Excel para gestion de clinicas. Costes, ventajas, limitaciones y casos de uso ideales para cada solucion.",
    metaKeywords: "CRM medico, Excel clinica, software gestion clinica, base de datos pacientes",
    excerpt: "Excel o CRM medico especializado? Analisis objetivo de costes, capacidades y ROI real. Descubre cuando tiene sentido cada opcion segun el tamano de tu clinica.",
    content: `
      <article class="prose max-w-none">
        <h2>La Pregunta de 10.000EUR: Excel vs CRM Especializado</h2>
        
        <p>Muchas clinicas comienzan con Excel. Es familiar, "gratis" (si ignoras el coste de Office 365), y parece suficiente al principio. Pero cuando deja de serlo? Y mas importante: cuanto te esta costando realmente quedarte en Excel?</p>

        <h3>Excel: Las Ventajas Reales</h3>

        <div class="bg-green-50 p-6 rounded-lg my-8">
          <h4 class="text-green-900 font-bold">Cuando Excel Tiene Sentido</h4>
          <ul>
            <li>Clinica unipersonal con menos de 50 pacientes activos</li>
            <li>Practica muy simple (consultas unicas, sin seguimiento)</li>
            <li>Presupuesto inicial extremadamente limitado</li>
            <li>Necesitas solo registro basico de contactos</li>
          </ul>
        </div>

        <h3>Excel: Las Limitaciones Criticas</h3>

        <h4>1. Escalabilidad Nula</h4>
        <p>Con 200+ pacientes, buscar un historial puede tomar 2-3 minutos. Multiplica por 20 busquedas diarias = 1 hora perdida. Al ano: 240 horas (30 dias laborales perdidos).</p>

        <h4>2. Riesgo de Perdida de Datos</h4>
        <p>Excel no tiene backup automatico ni historial de cambios robusto. Un archivo corrupto = perdida total. Has hecho backup hoy? Esta semana?</p>

        <h4>3. Imposibilidad de Automatizacion</h4>
        <p>No puede enviar recordatorios automaticos, generar facturas, o alertar de seguimientos pendientes. Todo requiere intervencion manual.</p>

        <h4>4. Colaboracion Caotica</h4>
        <p>Multiples personas editando el mismo Excel = caos garantizado. Versiones conflictivas, cambios sobrescritos, confusion total.</p>

        <h4>5. Zero Mobile</h4>
        <p>Editar Excel en el movil es una pesadilla. En 2025, tu sistema debe ser mobile-first.</p>

        <h3>CRM Medico: Las Ventajas Tangibles</h3>

        <h4>1. Ahorro de Tiempo Brutal</h4>
        <p>Busquedas instantaneas, historial completo en 1 click, formularios pre-rellenados. Ahorro estimado: 10-15 horas semanales en una clinica mediana.</p>

        <h4>2. Automatizacion que Trabaja 24/7</h4>
        <ul>
          <li>Recordatorios automaticos por WhatsApp/Email</li>
          <li>Alertas de seguimiento</li>
          <li>Facturacion automatica</li>
          <li>Reportes mensuales auto-generados</li>
        </ul>

        <h4>3. Insights de Negocio</h4>
        <p>Que tratamientos son mas rentables? Que fuente trae mas pacientes? Cual es tu tasa de retencion? Un CRM responde esto en segundos con dashboards visuales.</p>

        <h4>4. Seguridad y Cumplimiento RGPD</h4>
        <p>Backup automatico diario, cifrado, logs de auditoria, gestion de consentimientos. Todo incluido y conforme a normativa.</p>

        <h4>5. Escalabilidad Infinita</h4>
        <p>10 pacientes o 10.000, el sistema funciona igual de rapido. Multiples sedes, varios doctores, sin problema.</p>

        <h3>Comparativa de Costes Reales</h3>

        <table class="w-full border-collapse my-8">
          <thead>
            <tr class="bg-gray-100">
              <th class="border p-3 text-left">Concepto</th>
              <th class="border p-3 text-left">Excel</th>
              <th class="border p-3 text-left">CRM Medico</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="border p-3">Coste software/mes</td>
              <td class="border p-3">12EUR (Office 365)</td>
              <td class="border p-3">600EUR</td>
            </tr>
            <tr>
              <td class="border p-3">Tiempo administrativo/mes</td>
              <td class="border p-3">80h (2.000EUR)</td>
              <td class="border p-3">20h (500EUR)</td>
            </tr>
            <tr>
              <td class="border p-3">No-shows evitables/mes</td>
              <td class="border p-3">~3.000EUR perdidos</td>
              <td class="border p-3">~500EUR perdidos</td>
            </tr>
            <tr>
              <td class="border p-3">Setup IT inicial</td>
              <td class="border p-3">0EUR</td>
              <td class="border p-3">0EUR (cloud)</td>
            </tr>
            <tr class="font-bold bg-gray-50">
              <td class="border p-3">Coste real mensual</td>
              <td class="border p-3">~5.012EUR</td>
              <td class="border p-3">~1.600EUR</td>
            </tr>
          </tbody>
        </table>

        <p class="text-2xl font-bold text-teal-700 my-8">Ahorro neto con CRM: 3.412EUR/mes = 40.944EUR/ano</p>

        <h3>El Punto de Inflexion</h3>

        <p>Segun nuestro analisis de 200+ clinicas, el momento de cambiar llega cuando:</p>
        <ul>
          <li>Tienes mas de 100 pacientes activos</li>
          <li>Mas de 2 personas acceden a la base de datos</li>
          <li>Haces seguimientos recurrentes (ej: ortodoncia, implantes)</li>
          <li>El tiempo administrativo supera 10h semanales</li>
          <li>Has perdido datos al menos una vez</li>
        </ul>

        <blockquote class="border-l-4 border-teal-600 pl-6 italic my-8">
          "Resistimos el cambio durante 2 anos por 'ahorrar' 600EUR/mes. Cuando finalmente migramos, nos dimos cuenta que nos habia costado mas de 50.000EUR en ineficiencias."
          <footer class="text-sm text-gray-600 mt-2">- Dr. Javier M., Centro Oftalmologico Madrid</footer>
        </blockquote>

        <h3>Transicion: Mas Facil de lo que Piensas</h3>

        <p>El miedo #1 es: "La migracion sera un caos". Realidad:</p>
        <ul>
          <li>Import de Excel a CRM: 2-3 horas</li>
          <li>Formacion del equipo: 1 tarde</li>
          <li>Periodo de adaptacion: 1 semana</li>
          <li>ROI positivo: Mes 1</li>
        </ul>

        <h3>Veredicto Final</h3>

        <p><strong>Usa Excel si:</strong></p>
        <ul>
          <li>Eres unipersonal con menos de 50 pacientes</li>
          <li>Tu practica es extremadamente simple</li>
          <li>Solo necesitas un listin de contactos glorificado</li>
        </ul>

        <p><strong>Migra a CRM si:</strong></p>
        <ul>
          <li>Tienes 100+ pacientes</li>
          <li>Valoras tu tiempo en mas de 25EUR/hora</li>
          <li>Quieres crecer tu practica</li>
          <li>Te importa la experiencia del paciente</li>
          <li>Quieres dormir tranquilo sobre la seguridad de tus datos</li>
        </ul>

        <h3>Conclusion</h3>

        <p>Excel es una herramienta brillante... para hojas de calculo. Pero tu clinica no es una hoja de calculo, es un negocio complejo que merece herramientas disenadas especificamente para el.</p>

        <p>La pregunta real no es "puedo permitirme un CRM?" sino "puedo permitirme NO tenerlo?"</p>
      </article>
    `,
    coverImage: null,
    author: "Ing. Laura Gomez",
    publishedAt: new Date("2025-01-28"),
    updatedAt: new Date("2025-01-28"),
    tags: ["CRM medico", "Excel", "software clinicas", "comparativa", "ROI"],
  },
];

const faqs: InsertFaq[] = [
  {
    question: "Cuanto tiempo tarda la implementacion de Popoio?",
    answer: "La implementacion completa toma entre 7-10 dias. Esto incluye: migracion de datos (1-2 dias), configuracion personalizada (2-3 dias), formacion del equipo (1 sesion de 2 horas), y periodo de adaptacion con soporte intensivo (1 semana). La mayoria de clinicas estan operando completamente en el nuevo sistema en menos de 2 semanas.",
    category: "Implementacion",
    order: 1,
  },
  {
    question: "Necesito conocimientos tecnicos para usar Popoio?",
    answer: "No. Popoio esta disenado para ser tan intuitivo como tu app favorita de smartphone. Si sabes usar WhatsApp, sabes usar Popoio. Nuestro equipo de diseno ha trabajado especificamente para que cualquier persona, sin formacion tecnica previa, pueda dominar el sistema en menos de una tarde. Ademas, ofrecemos formacion inicial y soporte continuo.",
    category: "Uso",
    order: 2,
  },
  {
    question: "Mis datos estan seguros? Cumplen con RGPD?",
    answer: "Absolutamente. Popoio cumple 100% con el RGPD europeo. Tus datos estan cifrados de extremo a extremo, almacenados en servidores europeos certificados, con backup diario automatico. Incluimos gestion de consentimientos, derecho al olvido automatizado, y logs de auditoria completos. Ademas, firmamos acuerdos de confidencialidad y somos procesadores de datos oficiales segun normativa.",
    category: "Seguridad",
    order: 3,
  },
  {
    question: "Puedo migrar mis datos desde Excel u otro sistema?",
    answer: "Si, sin problema. Nuestro equipo se encarga de toda la migracion. Solo necesitamos tu archivo Excel (o export de tu sistema actual) y en 24-48 horas tendras todos tus datos importados, limpios y listos para usar. La migracion incluye: pacientes, historial de citas, tratamientos, y cualquier informacion relevante. Y lo mejor: es completamente gratis como parte del onboarding.",
    category: "Implementacion",
    order: 4,
  },
  {
    question: "Que pasa si cancelo? Pierdo mis datos?",
    answer: "Nunca. Tus datos son tuyos, siempre. Si decides cancelar, exportamos toda tu base de datos en formatos estandar (Excel, CSV, PDF) para que puedas llevartela donde quieras. No hay periodos de permanencia obligatorios ni penalizaciones. Puedes cancelar en cualquier momento con simplemente 1 mes de aviso.",
    category: "Precios",
    order: 5,
  },
  {
    question: "El precio incluye actualizaciones y nuevas funcionalidades?",
    answer: "Si. El precio mensual incluye todas las actualizaciones, nuevas funcionalidades, mejoras de seguridad, y soporte tecnico. No hay costes ocultos ni upgrades de pago. Cuando desarrollamos una nueva feature, todos los clientes la reciben automaticamente sin coste adicional.",
    category: "Precios",
    order: 6,
  },
  {
    question: "Funciona en movil y tablet?",
    answer: "Perfectamente. Popoio esta disenado mobile-first. Funciona de forma nativa en iPhone, Android, tablets, y ordenadores. La misma cuenta, sincronizada en tiempo real en todos tus dispositivos. Puedes revisar agendas, historiales de pacientes, y gestionar citas desde cualquier lugar, incluso sin conexion a internet (se sincroniza automaticamente cuando recuperas conexion).",
    category: "Uso",
    order: 7,
  },
  {
    question: "Puedo probar Popoio antes de comprometerme?",
    answer: "Si. Ofrecemos una demostracion personalizada de 30 minutos donde te mostramos el sistema con datos de ejemplo de tu tipo de clinica. Ademas, el primer mes incluye garantia de satisfaccion: si no estas contento por cualquier razon, te devolvemos el 100% del pago. Sin preguntas.",
    category: "Precios",
    order: 8,
  },
  {
    question: "Cuantos usuarios pueden acceder al sistema?",
    answer: "En el Plan Basico (600EUR/mes): hasta 3 usuarios simultaneos. En el Plan Personalizado: usuarios ilimitados. Cada usuario tiene su propio login y permisos configurables (ej: recepcionista solo ve agenda, doctor ve todo, administrador gestiona facturacion).",
    category: "Funcionalidades",
    order: 9,
  },
  {
    question: "Los recordatorios por WhatsApp tienen coste adicional?",
    answer: "En el Plan Basico incluimos recordatorios por Email ilimitados. Los recordatorios por WhatsApp estan disponibles en el Plan Personalizado sin coste adicional hasta 1.000 mensajes/mes (suficiente para la mayoria de clinicas). Volumenes superiores tienen un pequeno coste variable segun uso real.",
    category: "Funcionalidades",
    order: 10,
  },
  {
    question: "Ofrecen formacion para mi equipo?",
    answer: "Si. Todos los planes incluyen formacion inicial completa (1-2 sesiones online de 2 horas). Ademas, tenemos una biblioteca de videos tutoriales, guias paso a paso, y soporte por chat en directo durante horario laboral. Para clinicas con 5+ usuarios, ofrecemos formacion presencial bajo pedido.",
    category: "Implementacion",
    order: 11,
  },
  {
    question: "Popoio funciona para clinicas con multiples sedes?",
    answer: "Si, perfectamente. El Plan Personalizado esta disenado especificamente para esto. Puedes gestionar multiples sedes desde la misma cuenta, con agendas independientes pero datos centralizados. Ideal para grupos clinicos, franquicias, o profesionales con varias consultas.",
    category: "Funcionalidades",
    order: 12,
  },
  {
    question: "Necesito contratar servicios de hosting o servidores?",
    answer: "No. Popoio es 100% cloud. No necesitas comprar servidores, contratar IT, ni preocuparte por mantenimiento tecnico. Todo esta incluido en el precio mensual. Nosotros nos encargamos de servidores, backups, seguridad, actualizaciones, y toda la infraestructura tecnica.",
    category: "Implementacion",
    order: 13,
  },
  {
    question: "Puedo personalizar los recordatorios y mensajes automaticos?",
    answer: "Completamente. Puedes personalizar: tono del mensaje, timing (cuando se envian), canal (email/WhatsApp/SMS), y contenido especifico segun tipo de cita. Por ejemplo: recordatorios de limpieza dental vs ortodoncia pueden tener mensajes completamente diferentes y personalizados a tu marca.",
    category: "Funcionalidades",
    order: 14,
  },
  {
    question: "Hay limite de pacientes que puedo gestionar?",
    answer: "En el Plan Basico: hasta 500 pacientes activos. En el Plan Personalizado: pacientes ilimitados. Un 'paciente activo' es alguien con al menos una cita en los ultimos 24 meses. Pacientes antiguos sin actividad reciente no cuentan para el limite.",
    category: "Funcionalidades",
    order: 15,
  },
];

async function seedDatabase() {
  console.log("Iniciando seed de la base de datos...");

  try {
    console.log("Insertando articulos de blog...");
    for (const article of blogArticles) {
      await storage.createBlogArticle(article);
      console.log(`Articulo creado: ${article.title}`);
    }

    console.log("\nInsertando FAQs...");
    for (const faq of faqs) {
      await storage.createFaq(faq);
      console.log(`FAQ creada: ${faq.question}`);
    }

    console.log("\nSeed completado exitosamente!");
    console.log(`   - ${blogArticles.length} articulos de blog`);
    console.log(`   - ${faqs.length} FAQs`);
    
    process.exit(0);
  } catch (error) {
    console.error("Error durante el seed:", error);
    process.exit(1);
  }
}

seedDatabase();
```

---

### `client/index.html`
```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1" />
    <title>Popoio - Gestion Digital para Clinicas Medicas</title>
    <meta name="description" content="Software de gestion clinica version 2.0. CRM, paneles de control y alertas automaticas para clinicas dentales, oftalmologia, estetica y fisioterapia." />
    <meta name="keywords" content="software medico, gestion clinica, CRM medico, software dental, software clinica, transformacion digital clinicas, recordatorios WhatsApp, agenda medica, software sanitario Espana" />
    <link rel="canonical" href="https://popoio.com/" />
    
    <meta property="og:type" content="website" />
    <meta property="og:title" content="Popoio - Gestion Digital para Clinicas Medicas" />
    <meta property="og:description" content="Software de gestion clinica version 2.0. CRM, paneles de control y alertas automaticas para clinicas dentales, oftalmologia, estetica y fisioterapia." />
    <meta property="og:url" content="https://popoio.com/" />
    <meta property="og:site_name" content="Popoio" />
    <meta property="og:locale" content="es_ES" />
    
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content="Popoio - Gestion Digital para Clinicas Medicas" />
    <meta name="twitter:description" content="Software de gestion clinica version 2.0. CRM, paneles de control y alertas automaticas para clinicas dentales, oftalmologia, estetica y fisioterapia." />
    
    <link rel="icon" type="image/png" href="/favicon.png" />
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap" rel="stylesheet">
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "Organization",
      "name": "Popoio",
      "url": "https://popoio.com",
      "logo": "https://popoio.com/favicon.png",
      "description": "Software de gestion digital para clinicas medicas en Espana",
      "address": {
        "@type": "PostalAddress",
        "addressCountry": "ES"
      },
      "contactPoint": {
        "@type": "ContactPoint",
        "contactType": "Sales",
        "email": "diogo@468cap.com"
      }
    }
    </script>
  </body>
</html>
```

---

### `client/src/main.tsx`
```tsx
import { createRoot } from "react-dom/client";
import App from "./App";
import "./index.css";

createRoot(document.getElementById("root")!).render(<App />);
```

---

### `client/src/App.tsx`
```tsx
import { Switch, Route } from "wouter";
import { queryClient } from "./lib/queryClient";
import { QueryClientProvider } from "@tanstack/react-query";
import { Toaster } from "@/components/ui/toaster";
import { TooltipProvider } from "@/components/ui/tooltip";
import NotFound from "@/pages/not-found";
import Home from "@/pages/home";
import Login from "@/pages/login";
import Dashboard from "@/pages/dashboard";
import Blog from "@/pages/blog";
import BlogArticle from "@/pages/blog-article";
import FAQPage from "@/pages/faq";

function Router() {
  return (
    <Switch>
      <Route path="/" component={Home} />
      <Route path="/login" component={Login} />
      <Route path="/dashboard" component={Dashboard} />
      <Route path="/blog" component={Blog} />
      <Route path="/blog/:slug" component={BlogArticle} />
      <Route path="/faq" component={FAQPage} />
      <Route component={NotFound} />
    </Switch>
  );
}

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <TooltipProvider>
        <Toaster />
        <Router />
      </TooltipProvider>
    </QueryClientProvider>
  );
}

export default App;
```

---

### `client/src/index.css`
```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:is(.dark *));

@theme inline {
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  
  --color-background: hsl(var(--background));
  --color-foreground: hsl(var(--foreground));
  
  --color-primary: hsl(var(--primary));
  --color-primary-foreground: hsl(var(--primary-foreground));
  
  --color-secondary: hsl(var(--secondary));
  --color-secondary-foreground: hsl(var(--secondary-foreground));
  
  --color-muted: hsl(var(--muted));
  --color-muted-foreground: hsl(var(--muted-foreground));
  
  --color-accent: hsl(var(--accent));
  --color-accent-foreground: hsl(var(--accent-foreground));
  
  --color-card: hsl(var(--card));
  --color-card-foreground: hsl(var(--card-foreground));
  
  --color-popover: hsl(var(--popover));
  --color-popover-foreground: hsl(var(--popover-foreground));
  
  --color-border: hsl(var(--border));
  --color-input: hsl(var(--input));
  --color-ring: hsl(var(--ring));
  
  --font-sans: 'DM Sans', 'Inter', sans-serif;
  
  --radius: 0.5rem;
}

:root {
  --background: 38 30% 96%; 
  --foreground: 176 60% 15%;
  --primary: 176 60% 25%;
  --primary-foreground: 38 30% 96%;
  --secondary: 38 40% 90%;
  --secondary-foreground: 176 60% 25%;
  --accent: 176 35% 85%;
  --accent-foreground: 176 60% 25%;
  --card: 0 0% 100%;
  --card-foreground: 176 60% 15%;
  --popover: 0 0% 100%;
  --popover-foreground: 176 60% 15%;
  --muted: 38 20% 90%;
  --muted-foreground: 176 30% 40%;
  --border: 176 20% 85%;
  --input: 176 20% 85%;
  --ring: 176 60% 25%;
  --radius: 0.75rem;
}

.dark {
  --background: 176 50% 10%;
  --foreground: 38 30% 96%;
  --primary: 176 50% 40%;
  --primary-foreground: 38 30% 96%;
  --secondary: 176 40% 15%;
  --secondary-foreground: 38 30% 96%;
  --accent: 176 40% 20%;
  --accent-foreground: 38 30% 96%;
  --card: 176 45% 12%;
  --card-foreground: 38 30% 96%;
  --popover: 176 45% 12%;
  --popover-foreground: 38 30% 96%;
  --muted: 176 30% 20%;
  --muted-foreground: 176 20% 70%;
  --border: 176 30% 20%;
  --input: 176 30% 20%;
  --ring: 176 50% 40%;
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply font-sans antialiased bg-background text-foreground;
  }
}
```

---

### `client/src/lib/queryClient.ts`
```ts
import { QueryClient, QueryFunction } from "@tanstack/react-query";

async function throwIfResNotOk(res: Response) {
  if (!res.ok) {
    const text = (await res.text()) || res.statusText;
    throw new Error(`${res.status}: ${text}`);
  }
}

export async function apiRequest(
  method: string,
  url: string,
  data?: unknown | undefined,
): Promise<Response> {
  const res = await fetch(url, {
    method,
    headers: data ? { "Content-Type": "application/json" } : {},
    body: data ? JSON.stringify(data) : undefined,
    credentials: "include",
  });

  await throwIfResNotOk(res);
  return res;
}

type UnauthorizedBehavior = "returnNull" | "throw";
export const getQueryFn: <T>(options: {
  on401: UnauthorizedBehavior;
}) => QueryFunction<T> =
  ({ on401: unauthorizedBehavior }) =>
  async ({ queryKey }) => {
    const res = await fetch(queryKey.join("/") as string, {
      credentials: "include",
    });

    if (unauthorizedBehavior === "returnNull" && res.status === 401) {
      return null;
    }

    await throwIfResNotOk(res);
    return await res.json();
  };

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      queryFn: getQueryFn({ on401: "throw" }),
      refetchInterval: false,
      refetchOnWindowFocus: false,
      staleTime: Infinity,
      retry: false,
    },
    mutations: {
      retry: false,
    },
  },
});
```

---

### `client/src/lib/utils.ts`
```ts
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

---

Los archivos de las paginas (home.tsx, blog.tsx, blog-article.tsx, faq.tsx, dashboard.tsx, login.tsx, not-found.tsx) y componentes (contact-form-dialog.tsx, navbar.tsx, footer.tsx) y UI (accordion.tsx, button.tsx, card.tsx, dialog.tsx, form.tsx, input.tsx, label.tsx, toast.tsx, toaster.tsx, tooltip.tsx) son exactamente los que estan en el proyecto actual. Copia cada archivo directamente desde el repositorio de Replit.

Para los hooks:
- `client/src/hooks/use-toast.ts` - Sistema de toast notifications
- `client/src/hooks/use-mobile.tsx` - Hook para detectar mobile breakpoint

---

## Notas importantes para la migracion

1. **Base de datos**: Necesitas una base de datos PostgreSQL. Puedes usar Neon (neon.tech), Supabase, o cualquier PostgreSQL. El driver usado es `@neondatabase/serverless` - si usas PostgreSQL normal, cambia `db/index.ts` para usar `drizzle-orm/node-postgres` en su lugar.

2. **Videos**: Los 6 archivos .mp4 en `attached_assets/generated_videos/` son necesarios para la pagina principal. Debes copiarlos manualmente.

3. **Logo**: El archivo `attached_assets/Popoio - Logo_1763637341361.png` es el logo del proyecto.

4. **Resend**: Necesitas una cuenta de Resend (resend.com) con el dominio popoio.com verificado para que los emails funcionen.

5. **nanoid**: El archivo `server/vite.ts` usa `nanoid`. Asegurate de instalarlo: `npm install nanoid`

6. **Para produccion**: Ejecuta `npm run build` y luego `npm start`.
