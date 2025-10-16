
# WAF Transformer Dataset Insights

This document provides a high-level overview of the normalized web traffic dataset used for training the WAF transformer model. The original logs were sourced from benign interactions with the DVWA, WebGoat, and Juice Shop web applications.

## 📊 Overall Statistics
- **Total Requests Analyzed:** `1,133,280`
- **Requests with a Body (e.g., POST, PUT):** `196,275`
- **Unique Endpoints (Paths):** `183`

## 📡 HTTP Method Distribution
| Method   |   Count | Percentage   |
|----------|---------|--------------|
| GET      | 1015205 | 89.58%       |
| POST     |  102506 | 9.05%        |
| PUT      |   15569 | 1.37%        |

## 🏆 Top 15 Most Frequent Endpoints
| Path                                        |   Count |
|---------------------------------------------|---------|
| /juice/rest/products/<NUM>/reviews          |  109369 |
| /service/lessonmenu.mvc                     |  108715 |
| /juice/rest/user/whoami                     |   80252 |
| /dvwa/vulnerabilities/sqli                  |   75650 |
| /juice/rest/basket/<NUM>                    |   67911 |
| /dvwa/login.php                             |   56787 |
| /service/hint.mvc                           |   53241 |
| /juice/rest/products/search                 |   32491 |
| /juice/api/Quantitys                        |   32491 |
| /juice/api/BasketItems                      |   26600 |
| /juice/api/Products/<NUM>                   |   25276 |
| /dvwa/index.php                             |   18930 |
| /dvwa/vulnerabilities/upload                |   18912 |
| /dvwa/logout.php                            |   18911 |
| /juice/rest/admin/application-configuration |   16618 |

## 💻 User-Agent Families
| OS Family   |   Count | Percentage   |
|-------------|---------|--------------|
| macOS / iOS |  342496 | 30.22%       |
| Linux       |  326270 | 28.79%       |
| Android     |  286070 | 25.24%       |
| Windows     |  178443 | 15.75%       |
| Other       |       1 | 0.00%        |

## 📜 Sample Normalized Sequences
The following are examples of the final normalized sequences fed into the model. Sensitive data, version numbers, and dynamic IDs have been replaced with generic tokens like `<ID>`, `<NUM>`, and `<VERSION>`.

```
GET /?- - User-Agent: Mozilla/<VERSION> (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/<VERSION> Safari/<VERSION>
GET /dvwa?- - User-Agent: Mozilla/<VERSION> (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/<VERSION> Safari/<VERSION>
GET /dvwa?- - User-Agent: Mozilla/<VERSION> (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/<VERSION> Safari/<VERSION>
GET /dvwa/login.php?- - User-Agent: Mozilla/<VERSION> (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/<VERSION> Safari/<VERSION>
GET /?- - User-Agent: Mozilla/<VERSION> (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/<VERSION> Safari/<VERSION>
```
