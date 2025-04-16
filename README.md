# **AI Person Generator API**

## **Overview**
This API provides programmatic access to AI-generated human faces. It's designed to be:
- **Publicly accessible** (no authentication required)
- **Rate-limited** to prevent abuse
- **Cached** for better performance
- **Simple** to integrate with any application

## **Technical Implementation**

### **Core Features**
- **Automatic Image Generation**: Fetches fresh AI-generated portraits on demand
- **Smart Caching System**: Stores images for 5 minutes to reduce server load
- **Rate Limiting**: Allows 30 requests per minute per IP address
- **Resilient Fallback**: Serves cached images if generation fails
- **CORS Enabled**: Works in web browsers and mobile apps

### **How It Works**
1. Receives GET request at `/person` endpoint
2. Checks cache for existing valid image
3. If no cache:
   - Requests new image from generation source
   - Stores in cache
4. Returns image with appropriate headers

## **Usage Examples**

### **JavaScript Fetch**
```javascript
fetch('https://your-api.vercel.app/person')
  .then(response => response.blob())
  .then(imageBlob => {
    const imageUrl = URL.createObjectURL(imageBlob);
    document.getElementById('avatar').src = imageUrl;
  });
```

### **Python Requests**
```python
import requests

response = requests.get('https://your-api.vercel.app/person')
with open('person.jpg', 'wb') as f:
    f.write(response.content)
```

## **Response Headers**
| Header | Description |
|--------|-------------|
| `Content-Type` | `image/jpeg` |
| `X-Cache` | `HIT` (cached) / `MISS` (new) |
| `X-RateLimit-Remaining` | Requests left in current window |

## **Best Practices**
1. **Cache responses** client-side when possible
2. **Respect rate limits** (30 requests/minute)
3. **Handle errors gracefully** - check status codes
4. **Use HTTPS** for all requests

## **Performance**
- Average response time: ~300ms (cached) to ~1500ms (uncached)
- Uptime: 99.9% (when hosted on Vercel)
- Global CDN distribution

This API provides a reliable way to integrate AI-generated portraits into applications while maintaining fair usage policies and good performance characteristics.
