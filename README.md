
📜 **A public API for generating AI-powered human faces**  

---

## **🚀 Features**  
✅ **No API keys required** – Free to use  
✅ **Cached responses** – Faster load times  
✅ **Rate-limited** – 30 requests/minute per IP  
✅ **Always available** – Fallback to cached images if the source fails  
✅ **Simple integration** – Returns images directly  

---

## **📡 API Endpoints**  

### **1. Get a Random AI-Generated Face**  
```http
GET /person
```  
**Response:**  
- Direct JPEG image  
- Headers:  
  - `X-Cache`: `HIT` (cached) / `MISS` (new)  
  - `X-RateLimit-Remaining`: Requests left  

**Example:**  
```javascript
fetch('https://facegen-api.vercel.app/person')
  .then(res => res.blob())
  .then(image => {
    document.getElementById('face').src = URL.createObjectURL(image);
  });
```  

### **2. Check API Status**  
```http
GET /status
```  
**Response:**  
```json
{
  "status": "online",
  "requests": 1423,
  "cacheHits": 956,
  "uptime": "5h 23m"
}
```  

---

## **⚙️ How It Works**  
1. **First Request** → Fetches a new AI-generated face  
2. **Subsequent Requests (5 min window)** → Serves cached version  
3. **If API fails** → Still returns the last cached image  
4. **Rate-Limited** → 30 reqs/IP/minute  

---

## **🛠️ Tech Stack**  
- **Node.js** + **Express** (Server)  
- **Axios** (HTTP requests)  
- **Node-Cache** (Caching)  
- **Vercel** (Serverless hosting)  

---

## **📂 Project Structure**  
```
/facegen-api  
├── index.js         # Main API logic  
├── package.json     # Dependencies  
├── vercel.json      # Vercel config  
└── README.md        # Documentation  
```  

---

## **🚀 Deploy Your Own (Free!)**  
1. **Fork this repo**  
2. **Deploy to Vercel**:  
   ```sh  
   vercel  
   ```  
3. **Done!** Your API will be live at `your-app.vercel.app`  

---

## **📜 License**  
MIT License - Free for personal and commercial use.  

---  

🌟 **Enjoy the API? Star the repo!** → [GitHub Repo](#) (replace with your link)  

---  

### **📌 Example Usage**  

#### **Frontend (HTML/JS)**  
```html  
<img id="face" width="300" />  
<script>  
  fetch('https://facegen-api.vercel.app/person')  
    .then(res => res.blob())  
    .then(img => {  
      document.getElementById('face').src = URL.createObjectURL(img);  
    });  
</script>  
```  

#### **Python**  
```python  
import requests  

response = requests.get("https://facegen-api.vercel.app/person")  
with open("face.jpg", "wb") as f:  
    f.write(response.content)  
```  

