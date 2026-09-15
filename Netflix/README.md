# Netflix System Design

## **Functional Requirements**

- User sign up / login.
- Browse movies and TV shows.
- Search for movies, TV shows, and genres.
- Play, pause, resume, and stop videos.
- Continue watching from the last position.
- Allow users to create and manage profiles.
- Display personalized recommendations.
- Store watch history and viewing progress.

## **Non-Functional Requirements**

- High availability (99.99%+ uptime).
- Low video startup latency.
- Horizontally scalable.
- Fault tolerant.
- Highly reliable with no data loss.
- Smooth video streaming with minimal buffering.
- Secure user accounts and payment information.
- Content should be available globally.
- Recommendation data can be eventually consistent.

## **Estimation**

DAU = 100 Million

Average watch time = 2 hours/user/day

Total viewing time daily = 200 Million hours

### **Concurrent Users**

Average concurrent viewers:

200 million hours × 60 ÷ 1440 minutes/day

≈ 8.3 Million concurrent viewers

Assuming peak traffic is approximately 2× average:

Peak concurrent viewers ≈ **16.6 Million**

### **Video Storage**

Assume Netflix has around 20,000 movies and TV shows.

Average video content size after encoding ≈ 10 GB per title.

Storage needed:

20,000 × 10 GB

≈ 200 TB

Since every title is stored in multiple video qualities/resolutions:

200 TB × 5 ≈ **1 PB**

Additional storage can be required for replicas and different encoded formats.

### **Streaming Traffic**

Assume average streaming bitrate = 5 Mbps.

Peak concurrent viewers ≈ 16.6 Million.

Peak bandwidth:

16.6M × 5 Mbps

≈ 83 Tbps

This large amount of video traffic should be handled by a **CDN**, rather than sending videos directly from the application servers.

### **Total Storage**

Video content ≈ 1 PB

User profiles, watch history, metadata, and other application data are much smaller compared to video storage.

Therefore, a rough initial estimate for Netflix-scale video storage is around:

**~1 PB+**

With multiple copies, different encodings, backups, and replicas, the actual storage requirement can be several petabytes.
