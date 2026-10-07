# BÁO CÁO KIỂM THỬ API

## 1. Thông tin chung

| Nội dung | Thông tin |
|---|---|
| **Tên dự án** | Test Collection of APIs |
| **Công cụ kiểm thử** | Postman |
| **API được kiểm thử** | DummyJSON |
| **Base URL** | `https://dummyjson.com` |
| **Phương thức kiểm thử** | API Testing |
| **Tester** | Phạm Văn Tiến Dũng |
| **Mã sinh viên** | 23010681 |
| **Ngày thực hiện** | 07/10/2026 |

DummyJSON là REST API cung cấp dữ liệu giả lập phục vụ cho testing và prototyping. Trong bài thực hành này, resource `Posts` được sử dụng để kiểm thử việc lấy danh sách bài viết, lấy một bài viết theo ID và xử lý trường hợp tài nguyên không tồn tại.

## 2. Mục tiêu

Mục tiêu của bài thực hành là sử dụng Postman để thực hiện kiểm thử API và đánh giá kết quả trả về.

Các nội dung được kiểm thử gồm:

- Gửi HTTP request bằng Postman.
- Kiểm tra HTTP Status Code.
- Kiểm tra cấu trúc dữ liệu JSON.
- Kiểm tra giá trị của các trường trong response.
- Kiểm tra trường hợp request thành công.
- Kiểm tra trường hợp tài nguyên không tồn tại.
- Sử dụng Post-response Scripts để tự động kiểm tra response.
- Tổng hợp kết quả kiểm thử.

## 3. Công cụ và môi trường kiểm thử

### 3.1. Công cụ

| Công cụ | Mục đích |
|---|---|
| Postman | Gửi request và thực hiện các assertion |
| DummyJSON | API được sử dụng làm đối tượng kiểm thử |

### 3.2. API

**Base URL:**

```text
https://dummyjson.com
```

**Resource được sử dụng:**

```text
/posts
```

Endpoint `/posts` được sử dụng để lấy danh sách posts. Endpoint `/posts/1` được sử dụng để lấy một post cụ thể.

Tham số `limit` được sử dụng trong TC01 để giới hạn số lượng posts trả về.

## 4. Phạm vi kiểm thử

Trong bài thực hành này, 3 test case được xây dựng:

| Test Case | Method | Endpoint | Mục đích | Expected Status |
|---|---|---|---|---|
| TC01 | GET | `/posts?limit=3` | Lấy danh sách posts | 200 OK |
| TC02 | GET | `/posts/1` | Lấy post có ID = 1 | 200 OK |
| TC03 | GET | `/posts/9999` | Kiểm tra post không tồn tại | 404 Not Found |

TC01 sử dụng `limit=3` để chỉ lấy 3 phần tử trong danh sách. Việc này giúp response ngắn gọn và dễ quan sát trong quá trình kiểm thử cũng như khi trình bày trong README.

## 5. Chi tiết các Test Case

## 5.1. TC01 – Get List of Posts

### 5.1.1. Mục đích

Kiểm tra API có thể trả về danh sách các bài viết và response có cấu trúc JSON đúng như mong đợi hay không.

### 5.1.2. Request

**Method:**

```text
GET
```

**URL:**

```text
https://dummyjson.com/posts?limit=3
```

### 5.1.3. Expected Result

Request được xem là thành công khi:

- HTTP Status Code bằng `200`.
- Response chứa trường `posts`.
- Trường `posts` có kiểu dữ liệu là `array`.
- Response chứa trường `total`.
- Giá trị `limit` bằng `3`.

### 5.1.4. Postman Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Posts is an array", function () {
    const data = pm.response.json();
    pm.expect(data.posts).to.be.an("array");
});

pm.test("Response contains total", function () {
    const data = pm.response.json();
    pm.expect(data).to.have.property("total");
});

pm.test("Limit is 3", function () {
    const data = pm.response.json();
    pm.expect(data.limit).to.eql(3);
});
```

### 5.1.5. Actual Result

API trả về:

```text
200 OK
```

Kết quả kiểm thử:

| Assertion | Result |
|---|---|
| Status code is 200 | PASS |
| Posts is an array | PASS |
| Response contains total | PASS |
| Limit is 3 | PASS |

**Test Results: 4/4 tests passed**

### 5.1.6. Screenshot

<img width="955" height="496" alt="TC01 - Get List of Posts" src="https://github.com/user-attachments/assets/27cac1b4-73a4-4440-ae10-aae571e5cd18" />

**Request:**

```text
GET https://dummyjson.com/posts?limit=3
```

**Test Results:** `4/4`

**Status:** `200 OK`

### 5.1.7. Response

<details>
<summary>Click để xem Response</summary>

```json
{
    "posts": [
        {
            "id": 1,
            "title": "His mother had always taught him",
            "body": "His mother had always taught him not to ever think of himself as better than others. He'd tried to live by this motto. He never looked down on those who were less fortunate or who had less money than him. But the stupidity of the group of people he was talking to made him change his mind.",
            "tags": [
                "history",
                "american",
                "crime"
            ],
            "reactions": {
                "likes": 192,
                "dislikes": 25
            },
            "views": 305,
            "userId": 121
        },
        {
            "id": 2,
            "title": "He was an expert but not in a discipline",
            "body": "He was an expert but not in a discipline that anyone could fully appreciate. He knew how to hold the cone just right so that the soft server ice-cream fell into it at the precise angle to form a perfect cone each and every time. It had taken years to perfect and he could now do it without even putting any thought behind it.",
            "tags": [
                "french",
                "fiction",
                "english"
            ],
            "reactions": {
                "likes": 859,
                "dislikes": 32
            },
            "views": 4884,
            "userId": 91
        },
        {
            "id": 3,
            "title": "Dave watched as the forest burned up on the hill.",
            "body": "Dave watched as the forest burned up on the hill, only a few miles from her house. The car had been hastily packed and Marta was inside trying to round up the last of the pets. Dave went through his mental list of the most important papers and documents that they couldn't leave behind. He scolded himself for not having prepared these better in advance and hoped that he had remembered everything that was needed. He continued to wait for Marta to appear with the pets, but she still was nowhere to be seen.",
            "tags": [
                "magical",
                "history",
                "french"
            ],
            "reactions": {
                "likes": 1448,
                "dislikes": 39
            },
            "views": 4152,
            "userId": 16
        }
    ],
    "total": 251,
    "skip": 0,
    "limit": 3
}
```

</details>

## 5.2. TC02 – Get a Single Post

### 5.2.1. Mục đích

Kiểm tra API có thể lấy chính xác một bài viết dựa trên ID hay không.

### 5.2.2. Request

**Method:**

```text
GET
```

**URL:**

```text
https://dummyjson.com/posts/1
```

### 5.2.3. Expected Result

Request được xem là thành công khi:

- HTTP Status Code bằng `200`.
- ID của post trả về bằng `1`.
- Response chứa trường `title`.
- Response chứa trường `body`.

### 5.2.4. Postman Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Post ID is 1", function () {
    const data = pm.response.json();
    pm.expect(data.id).to.eql(1);
});

pm.test("Response has title", function () {
    const data = pm.response.json();
    pm.expect(data).to.have.property("title");
});

pm.test("Response has body", function () {
    const data = pm.response.json();
    pm.expect(data).to.have.property("body");
});
```

### 5.2.5. Actual Result

API trả về:

```text
200 OK
```

Kết quả kiểm thử:

| Assertion | Result |
|---|---|
| Status code is 200 | PASS |
| Post ID is 1 | PASS |
| Response has title | PASS |
| Response has body | PASS |

**Test Results: 4/4 tests passed**

### 5.2.6. Screenshot

<img width="959" height="538" alt="TC02 - Get a Single Post" src="https://github.com/user-attachments/assets/6e5b8240-d2f8-40e5-8c97-daf644363d16" />

**Request:**

```text
GET https://dummyjson.com/posts/1
```

**Test Results:** `4/4`

**Status:** `200 OK`

### 5.2.7. Response

<details>
<summary>Click để xem Response</summary>

```json
{
    "id": 1,
    "title": "His mother had always taught him",
    "body": "His mother had always taught him not to ever think of himself as better than others. He'd tried to live by this motto. He never looked down on those who were less fortunate or who had less money than him. But the stupidity of the group of people he was talking to made him change his mind.",
    "tags": [
        "history",
        "american",
        "crime"
    ],
    "reactions": {
        "likes": 192,
        "dislikes": 25
    },
    "views": 305,
    "userId": 121
}
```

</details>

## 5.3. TC03 – Get a Non-existent Post

### 5.3.1. Mục đích

Kiểm tra khả năng xử lý lỗi của API khi client yêu cầu một tài nguyên không tồn tại.

Đây là một **negative test case**.

### 5.3.2. Request

**Method:**

```text
GET
```

**URL:**

```text
https://dummyjson.com/posts/9999
```

### 5.3.3. Expected Result

Do post có ID `9999` không tồn tại, API được kỳ vọng trả về:

```text
404 Not Found
```

Response cũng phải chứa thông tin lỗi với trường `message`.

### 5.3.4. Postman Test Script

```javascript
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Response contains error message", function () {
    const data = pm.response.json();
    pm.expect(data).to.have.property("message");
});
```

### 5.3.5. Actual Result

API trả về:

```text
404 Not Found
```

Kết quả kiểm thử:

| Assertion | Result |
|---|---|
| Status code is 404 | PASS |
| Response contains error message | PASS |

**Test Results: 2/2 tests passed**

> Lưu ý: Mặc dù HTTP Status Code là `404`, test case này vẫn được đánh giá là `PASS` vì `404` chính là kết quả mong đợi của TC03.

### 5.3.6. Screenshot

<img width="960" height="493" alt="TC03 - Get a Non-existent Post" src="https://github.com/user-attachments/assets/501151ad-00d2-4ce8-9b43-19ecfaa23088" />

**Request:**

```text
GET https://dummyjson.com/posts/9999
```

**Test Results:** `2/2`

**Status:** `404 Not Found`

### 5.3.7. Response

<details>
<summary>Click để xem Response</summary>

```json
{
    "message": "Post with id '9999' not found"
}
```

</details>

## 6. Tổng hợp kết quả kiểm thử

### 6.1. Kết quả theo Test Case

| Test Case | Expected Status | Actual Status | Assertions | Result |
|---|---|---|---|---|
| TC01 | 200 OK | 200 OK | 4/4 | PASS |
| TC02 | 200 OK | 200 OK | 4/4 | PASS |
| TC03 | 404 Not Found | 404 Not Found | 2/2 | PASS |

### 6.2. Tổng hợp Assertions

| Nội dung | Kết quả |
|---|---:|
| Total Test Cases | 3 |
| Total Assertions | 10 |
| Passed Assertions | 10 |
| Failed Assertions | 0 |
| Success Rate | 100% |

### Kết quả cuối cùng

**10/10 assertions PASSED**

**Success Rate: 100%**

## 7. Phân tích kết quả

### TC01

TC01 kiểm tra chức năng lấy danh sách posts. API trả về `200 OK`. Dữ liệu `posts` có kiểu `array`, response có trường `total` và tham số `limit` được trả về đúng bằng `3`.

Tất cả điều kiện đều đạt nên TC01 được đánh giá là **PASS**.

### TC02

TC02 kiểm tra chức năng lấy một post cụ thể. API trả về `200 OK`, ID của post bằng `1` và response chứa các trường cần thiết là `title` và `body`.

TC02 được đánh giá là **PASS**.

### TC03

TC03 thực hiện negative testing bằng cách yêu cầu post có ID `9999`, là một tài nguyên không tồn tại. API trả về `404 Not Found` và response chứa thông tin lỗi.

Đây chính là kết quả được mong đợi nên TC03 được đánh giá là **PASS**.

## 8. Nhận xét

Qua quá trình kiểm thử, API đã đáp ứng các yêu cầu được đặt ra trong cả ba test case.

Các test case bao phủ hai nhóm chính:

| Loại kiểm thử | Test Case | Nội dung |
|---|---|---|
| Positive Testing | TC01, TC02 | Kiểm tra các request hợp lệ |
| Negative Testing | TC03 | Kiểm tra request tới tài nguyên không tồn tại |

Việc sử dụng Postman Post-response Scripts giúp tự động hóa việc kiểm tra thay vì phải kiểm tra thủ công từng response.

Kết quả kiểm thử:

- Total Test Cases: 3
- Total Assertions: 10
- Passed Assertions: 10
- Failed Assertions: 0
- Success Rate: 100%

## 9. Kết luận

Bài thực hành đã sử dụng Postman để kiểm thử API DummyJSON thông qua ba test case.

Các nội dung đã thực hiện gồm:

- Gửi GET request.
- Kiểm tra HTTP Status Code.
- Kiểm tra cấu trúc JSON.
- Kiểm tra giá trị của dữ liệu trả về.
- Kiểm tra resource tồn tại.
- Kiểm tra resource không tồn tại.
- Sử dụng Post-response Script để tự động hóa kiểm thử.
- Tổng hợp và đánh giá kết quả kiểm thử.

Kết quả cuối cùng là **10/10 assertions PASSED**, đạt **100% tỷ lệ thành công** trong phạm vi các test case đã xây dựng.
