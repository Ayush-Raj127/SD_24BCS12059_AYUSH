# TinyURL System Design



## **Functional Requirements**

* Convert a long URL into a short URL (7-character alphanumeric string).
* Redirect users from the short URL to the original long URL.
* Allow users to view all URLs they have created.
* Display analytics for each URL (number of clicks, creation date, etc.).
* Support custom aliases (e.g., tinyurl.com/openai).
* Allow URL expiration (optional).
* Prevent duplicate short URLs.



## **Non-Functional Requirements**

* High availability (99.99%+ uptime).
* Low latency (<50–100 ms redirects).
* Horizontally scalable.
* Fault tolerant.
* Highly reliable (no data loss).
* Short URLs must be globally unique.
* Analytics can be eventually consistent.
* Secure against spam and malicious URLs.



## **Estimation**

DAU = 10 Million

One user creates two URLs daily.

Total URLs created daily = 20 Million



Each link is used for redirection 10 times a day.

Daily redirections = 200 Million

Requests per second ≈ 2314



### **Short URL Storage**

Short URL length = 7 characters

Characters available:

* A-Z = 26
* a-z = 26
* 0-9 = 10
* Total = 62 possibilities

Storage for one short URL ≈ 7 bytes

62^7 ≈ 3.5 trillion possible URLs



Storage needed per day:

7 bytes × 20 million ≈ 140 MB

Storage needed per year:

140 MB × 365 ≈ 51.1 GB

Storage needed for 10 years:

51.1 GB × 10 ≈ 511 GB



### **Long URL Storage**

Number of URLs created per day = 20 million

Average long URL size ≈ 200 bytes

Storage needed per day:

200 bytes × 20 million ≈ 4 GB

Storage needed per year:

4 GB × 365 ≈ 1.4 TB

Storage needed for 10 years:

1.4 TB × 10 ≈ 14 TB



### **Total Storage**

Short URL storage ≈ 0.5 TB

Long URL storage ≈ 14 TB

Total storage needed ≈ **15 TB for 10 years**



With database replication:

15 TB × 3 ≈ **45 TB total storage capacity for 10 years**
