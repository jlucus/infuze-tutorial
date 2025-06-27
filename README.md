# 🚀 Infuze Cloud Deployment Tutorial  
Infuze Web Hosting Tutorial: Getting Started With Infuze.Cloud

**Atomic deployments with zero-downtime rollbacks**  
[![Infuze Version](https://img.shields.io/badge/Infuze-1.2.0-3423A6)](https://npmjs.com/package/infuze) 
[![Deployment Time](https://img.shields.io/badge/Deployment_Time-<800ms-success)]()

```mermaid
graph LR
    A[Developer] -->|infuze deploy|B(Infuze Cloud)
    B --> C[Build Assets]
    C --> D[Compress]
    D --> E[Upload to CDN]
    E --> F[Update Routing]
    F --> G[Live Production]
```

## ⚙️ Installation & Setup

### 1. Install API Tool With NPM
```bash
npm install -g infuze
```

### 2. Initialize Project
```bash
cd your-website/
infuze init
```
```terminal
✔ Created infuze.config.js
✔ Connected to Infuze Cloud (API v3)
✔ Detected framework: Next.js
```

### 3. Configure Deployment
Edit `infuze.config.js`:
```javascript
export default {
  projectId: "WEBSITE_1X8F9K",
  build: {
    command: "npm run build",
    directory: "./out"
  },
  providers: [
    {
      type: "infuze-cloud", // Primary provider
      zone: "jlucus.dev"
    },
    {
      type: "aws-s3", // Backup provider
      bucket: "website-failover"
    }
  ],
  compression: {
    formats: ["brotli", "zstd"]
  }
}
```

## 🚦 Deployment Workflow

### 1. Test Locally
```bash
infuze preview
```
```terminal
🌐 Preview server: http://localhost:4173
📦 Assets built in 2.1s
✅ Compression: 42 files (original 1.7MB → 890KB)
```

### 2. Production Deployment
```bash
infuze deploy --env=production
```
```terminal
🚀 Starting deployment to [production]
🔑 Authenticated with Infuze Cloud (user@jlucus.dev)
🛠️ Running build: npm run build
📦 Generated 42 static assets (1.7MB)
🔥 Compressed: 890KB (48% reduction)
📡 Uploading to Infuze Global CDN...
✅ Deployment complete! (3.8s)
🌐 Production URL: https://www.jlucus.dev
🔗 Version URL: https://cdn.jlucus.dev/p/prod-1x8f9k
```

### 3. Verify Deployment
```bash
infuze status
```
```terminal
VERSION: prod-1x8f9k
STATUS: Active
DEPLOYED: 2023-11-15 14:30:22 UTC
SIZE: 890KB (42 files)
ENDPOINTS:
  • Primary: https://www.jlucus.dev
  • Failover: https://failover.jlucus.dev
```

### 4. Instant Rollback
```bash
infuze rollback prod-previous-version-id
```
```terminal
⚠️ Rolling back to prod-previous-version-id
🔄 Switching traffic in 300ms...
✅ Rollback complete! Zero downtime
```

## 🔐 Security Features
```mermaid
pie
    title Security Layers
    “TLS 1.3 Encryption” : 35
    “Content Integrity Checks” : 25
    “DDoS Protection” : 20
    “WAF Rules” : 20
```

## ⚡ Performance Optimization
Infuze automatically applies:
- Brotli/Zstd compression
- Cache-control headers
- HTTP/3 prioritization
- Critical CSS injection

## 🛠️ GitHub Actions Integration
`.github/workflows/deploy.yml`:
```yaml
name: Production Deploy
on: [push]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
      
      - name: Install Infuze
        run: npm install -g infuze
        
      - name: Deploy to Production
        run: infuze deploy --env=production
        env:
          INFUZE_API_KEY: ${{ secrets.INFUZE_KEY }}
```

## 📊 Monitoring (Post-Deploy)
```bash
infuze metrics
```
```terminal
REQUESTS (24h): 42,891
PERFORMANCE:
  • TTFB: 47ms avg
  • LCP: 820ms
  • Cache hit: 92%
ERROR RATE: 0.02%
```

## 🚨 Troubleshooting
```bash
# Inspect deployment logs:
infuze logs --deploy=prod-1x8f9k

# Verify file integrity:
infuze verify --version=prod-1x8f9k

# Emergency rollback:
infuze rollback last-stable --force
```

---
> **Get Started**  
> [Create Account](https://cloud.infuze.dev/signup) • 
> [Documentation](https://docs.infuze.dev) • 
> [api Reference](https://api.infuze.dev)

[![Deploy with Infuze](https://img.shields.io/badge/Deploy_Example_Site-3423A6?style=for-the-badge)](https://cloud.infuze.dev/deploy?template=nextjs)
```

---

### Key Features Showcased:
1. **Atomic Deployments**  
   - Version-pinned URLs (`cdn.jlucus.dev/p/prod-1x8f9k`)
   - Zero-downtime cutovers
   - Immutable releases

2. **Infuze Cloud Integration**  
   - Managed global CDN
   - Built-in DDoS protection
   - Automatic HTTP/3 support

3. **Visual Workflows**  
   - Mermaid deployment diagram
   - Security layers pie chart
   - Color-coded terminal output

4. **Enterprise-Grade Features**  
   - Multi-provider failover (Infuze + AWS S3)
   - Performance optimization pipeline
   - Real-time metrics monitoring

5. **DevOps Ready**  
   - GitHub Actions template
   - One-command rollbacks
   - Log inspection tools

---

### Recommended Repo Structure:
```
infuze-cloud-demo/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── public/
├── src/
├── infuze.config.js
├── package.json
└── README.md (this tutorial)
```

Save this as `README.md` in your demo repository. For immediate testing, create a live demo with:

```bash
npx create-infuze-app@latest my-demo-site
cd my-demo-site
infuze deploy --test
```

[Download this tutorial as markdown file](https://gist.githubusercontent.com/jlucus/infuze-tutorial/main/README.md)
