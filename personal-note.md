1. Hiểu dataset

- 60 ngày, gồm dữ liệu OHLCV (Open, High, Low, Closed, Volume) + ngày
  - Open:
    - giá vào lúc bắt đầu trong ngày
    - ảnh hưởng bởi supply + demand trong đêm
    - dùng để đánh giá mức độ/sự kiện ngoài giờ (gap = open - closed previous day)
  - High:
    - giá cao nhất trong ngày -> thể hiện sức mua tối đa
    - dùng để tính biến động trong ngày (intraday volatility)
  - Low:
    - giá thấp nhất -> sức bán tối thiểu (worst case to sell)
    - intraday volatility
    - range = High - Low
  - Closed:
    - giá kết thúc ngày
    - mục tiêu dự đoán
  - Volume:
    - tổng số share trao đổi -> ~ tích phân
    - trend
    - volatility shifts
    - breakout

2. Mục tiêu

- Dự đoán Closed trong tương lai (1 ngày/nhiều ngày)
  - Raw: Closed(t + 1)
  - Return: $r_t = \dfrac{Closed_{t} - Closed_{t-1}}{Closed_{t-1}}$
  - Log return: $l_t = \log (\dfrac{Closed_t}{Closed_{t-1}})$

3. Train/Test data

- Train data:
  - Input: features 45 days (1 - 45)
  - Output: closed 45 days (2 - 46)
- Test data:
  - Input: features 14 days (46 - 59)
  - Output: closed 14 days (47 - 60)
- Target:
  - Closed day 60

4. Exploratory Data Analysis (EDA)

- Tải và xem xét dữ liệu (các cột, thông tin các cột, missing values,...)
- Trực quan hóa dữ liệu (các cột, các feature suy ra từ các cột)
  - Cột 'Close': trend, spike, unusual jump?
  - Daily returns (phần trăm so với ngày trước) -> ổn định hơn so với raw price
  - Volume: Spike xuống <-> Spike lên của close price
  - Tương quan: OHLC tương quan ~ 1, còn Volume không liên quan mấy (corr < 0)
