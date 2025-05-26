If you’re already using **Google Cloud** and **Firebase**, integrating alternatives to Cloudflare becomes easier since Google’s ecosystem offers native tools that minimize reliance on third-party services. Below is a revised strategy tailored to your stack, balancing security, performance, and user experience without intrusive CAPTCHAs.

---

### **Google-Native Alternatives**
Leverage Google’s infrastructure for seamless integration with Firebase and reduced complexity:

#### 1. **Google Cloud CDN + Cloud Armor**  
   - **Google Cloud CDN**: Built for speed and scalability, integrates directly with Firebase Hosting, Compute Engine, or GKE.  
   - **Cloud Armor**: Google’s WAF and DDoS protection service.  
     - Configure custom security policies (e.g., block malicious IPs, geo-restrictions).  
     - Use **Adaptive Protection** (AI-based DDoS mitigation) instead of CAPTCHAs.  
   - **Pros**: Minimal latency, no CAPTCHAs, and native Firebase compatibility.  

#### 2. **Firebase Hosting + Cloud Functions**  
   - **Firebase Hosting**: Already includes global CDN, SSL, and DDoS protection at the edge.  
   - **Cloud Functions**: Add serverless security logic (e.g., rate limiting, bot detection) via Firebase Triggers.  
     - Example: Use a Cloud Function to block suspicious requests before they hit your app.  

#### 3. **Google Cloud Load Balancing**  
   - Distribute traffic globally with built-in DDoS protection.  
   - Pair with **Cloud Armor** for advanced WAF rules (e.g., block SQLi, XSS).  

#### 4. **reCAPTCHA Enterprise**  
   - Google’s less intrusive alternative to traditional CAPTCHAs.  
   - Integrates with Firebase Auth and Cloud Armor to detect bots without annoying users.  

---

### **Third-Party Integrations for Google Cloud**
If you need additional features, these tools work smoothly with Google Cloud:

#### 1. **Fastly (CDN + Security)**  
   - Edge platform with real-time logging and custom VCL rules for traffic filtering.  
   - Integrates with Firebase via **Google Cloud Load Balancer** (GCLB).  
   - **Key Feature**: Advanced bot mitigation with behavioral analysis (no CAPTCHAs).  

#### 2. **Sucuri (WAF + CDN)**  
   - Lightweight WAF that sits in front of Firebase Hosting.  
   - Blocks bad traffic at the DNS level (CNAME setup) with minimal user friction.  

#### 3. **BunnyCDN**  
   - Affordable CDN with DDoS protection.  
   - Works alongside Firebase Hosting for static assets (e.g., images, videos).  

---

### **Manual Security for Firebase/Google Cloud**
For granular control without CAPTCHAs:

#### 1. **WAF/Rate Limiting**  
   - **Cloud Armor**: Create rules to block IPs, regions, or request patterns (e.g., excessive API calls).  
   - **Firebase App Check**: Enforce that only your apps (iOS/Android/web) can access Firebase resources.  

#### 2. **Bot Mitigation**  
   - **reCAPTCHA Enterprise**: Detect bots via risk scores (no user interaction).  
   - **Cloud Functions**: Deploy custom logic to:  
     - Analyze headers (e.g., `User-Agent`, `Referer`).  
     - Block headless browsers (e.g., Puppeteer, Selenium).  

#### 3. **DDoS Protection**  
   - **Google Cloud Armor Adaptive Protection**: Automatically detects and mitigates volumetric attacks.  
   - **VPC Firewall Rules**: Restrict traffic to your Compute Engine VMs.  

#### 4. **DNS Security**  
   - **Google Cloud DNS**: Enable DNSSEC and restrict zone transfers.  
   - **Private Google Access**: Secure Firebase Realtime Database/Cloud Firestore endpoints.  

---

### **Example Architecture**  
Here’s how to piece it together:  
```
User → Google Cloud CDN (cached assets) → Firebase Hosting (static content)  
         ↓  
Cloud Load Balancer (SSL termination) → Cloud Armor (WAF rules)  
         ↓  
Cloud Run/Compute Engine (backend) + Firebase Auth/App Check  
         ↓  
Cloud Functions (security logic) + Firestore (database)  
```

---

### **Key Recommendations**  
1. **Start with Google Native Tools**: Use **Cloud Armor + Cloud CDN** for WAF/DDoS and **Firebase Hosting** for static content.  
2. **Add reCAPTCHA Enterprise**: For high-risk endpoints (e.g., login, signup).  
3. **Avoid Over-Engineering**: Only add third-party tools (e.g., Fastly) if you need advanced bot logic or multi-CDN.  
4. **Monitor with Google Operations Suite**: Track traffic anomalies and set alerts for attacks.  

By prioritizing Google’s ecosystem, you reduce complexity while maintaining strong security and a smooth user experience.