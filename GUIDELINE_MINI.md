# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.
> Tọa độ trong bảng ca mơ hồ là pixel (x1, y1, x2, y2) trên ảnh 640×640.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` (0) | Xe con chở người: sedan, hatchback, SUV/crossover, taxi, xe bán tải cabin nhỏ | Có nắp capô rõ, thân thấp; mui ngắn hơn nửa chiều dài xe. |
| `truck` (1) | Xe chở hàng có cabin tách biệt thùng hàng: xe tải thùng, xe ben, xe đầu kéo, xe cứu hộ, xe chuyên dụng | Thấy khe/khối tách giữa cabin và thùng; thùng hở chở đất/hàng, thùng kín cao hơn cabin. |
| `bus` (2) | Xe chở khách nhiều cửa, nhiều hàng cửa sổ dài liên tục: xe buýt thường, buýt nối toa, buýt 2 tầng, minibus | Dài gấp nhiều lần xe con, . Buýt nối toa là một box gồm cả hai toa |
| `van` (3) | Xe thân hộp một khối: van chở hàng, minivan chở người, xe 16 chỗ cỡ nhỏ | Mũi xe ngắn/dốc, mui cao kéo thẳng tới đuôi, cửa trượt hông. Ngắn hơn bus, không có đèn sáng tuyến |

## Quy tắc chung

- **Box bám sát vật thể** nghĩa là: 4 cạnh chạm điểm ngoài cùng của thân xe nhìn thấy (gồm gương, cản, thùng hàng); không lấy bóng đổ, vệt đèn, mặt đường hay xe bên cạnh. 
- **Vật thể bị che khuất**: vẫn gán nếu phần nhìn thấy đủ nhận ra lớp; box chỉ bao phần nhìn thấy, không đoán phần bị che. Hai xe chồng nhau thì sẽ có hai box riêng.
- **Vật thể bị cắt bởi rìa ảnh**: gán box kéo đúng tới rìa ảnh; không ngoại suy phần ngoài khung. Gán lớp theo phần còn thấy.
- **Vật thể rất nhỏ/mơ hồ**: gán nếu nhận ra được là xe thuộc 4 lớp. Nhỏ hơn, hoặc mờ tới mức không phân biệt được lớp thì không gán.
- **Không gán**: người đi bộ, xe đạp, mô tô/xe máy, xe ba bánh, biển báo, xe trong ảnh quảng cáo/phản chiếu.
- Lớp mô tả loại xe, không phụ thuộc trạng thái.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_023` | Xe buýt 2 tầng đỏ–trắng ở mép phải, bị rìa phải và rìa trên cắt mất phần lớn thân; chỉ thấy hông xe có quảng cáo | Gán `bus` , box kéo tới rìa phải và rìa trên ảnh | Phần nhìn thấy (hai tầng cửa sổ, thân dài, quảng cáo hông) đủ nhận diện xe khách cỡ lớn → `bus`. Theo quy tắc cắt khung: box chạm rìa, không đoán phần ngoài ảnh |
| `drive_039` | Xe ben chở đất chạy sát và che một phần buýt nối toa vàng; bên trái có buýt nối toa khác bị rìa trái cắt | Xe ben → `truck`; mỗi xe buýt là một box `bus`  trên phần nhìn thấy | Xe ben có cabin tách thùng hở chở hàng là `truck`. Buýt bị che vẫn nhận ra được (bảng tuyến LED, cửa sổ dài) thì gán phần thấy được. Buýt nối toa là một phương tiện → một box, không tách theo toa |
| `drive_026` | Xe trắng thân cao, mui dài, có giá nóc có thể nhầm `van` | Gán `car` | Phóng to thấy capô dài rõ, kính lái nghiêng, đuôi ngắn |
| `drive_026` | Xe trắng–xanh làn bên phải có cần kéo phía sau, giống van chuyên dụng | Gán `truck` | Là xe cứu hộ: cabin phía trước tách với sàn/cần kéo phía sau, dùng chở/kéo xe chứ không chở khách → `truck`, không phải `van` |
