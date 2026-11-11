# 🎯 Phi Tiêu Điện Thoại

Phone-as-dart-thrower: màn hình lớn hiện bia, mỗi người quét QR và dùng điện thoại ngắm + vung tay ném. 2–6 người, 3 lượt × 3 phi tiêu.

## Chạy
- **Phải qua HTTPS** (cảm biến điện thoại không chạy trên http/file). Cách nhanh nhất: GitHub Pages.
- Mở `index.html` trên laptop/TV → quét QR bằng điện thoại.
- Test solo không cần điện thoại: bấm **Thử bằng chuột** (di chuột = ngắm, click = ném).

## Deploy GitHub Pages
```bash
git init && git add . && git commit -m "Phi Tieu Dien Thoai v0.1"
git branch -M main
git remote add origin https://github.com/haiduy2405/dart-thrower.git
git push -u origin main
```
Repo → Settings → Pages → Branch `main` / root. URL: `https://haiduy2405.github.io/dart-thrower/`

## Cách chơi
1. Điện thoại: nhập tên → **Vào chơi** (iOS sẽ hỏi quyền cảm biến → Cho phép).
2. Cầm như remote TV, hướng vào bia → bấm **Căn giữa**.
3. Đến lượt: viền sáng lên → vung tay như ném phi tiêu. Lực vừa phải (~24 m/s²) bay thẳng; yếu thì rơi thấp, mạnh quá thì bay cao.
4. Máy không có cảm biến: vuốt lên trên màn hình để ném.

## Chỉnh độ nhạy
| Hằng số | File | Ý nghĩa |
|---|---|---|
| `RANGE` | play.html | Độ quay (°) = 1 bán kính bia. Nhỏ hơn = nhạy hơn |
| `TH` | play.html | Ngưỡng gia tốc nhận cú ném. Cao hơn = phải vung mạnh hơn |
| `LOOKBACK` | play.html | Bù trễ (ms) toạ độ ngắm trước cú vung |
| `SWEET` | index.html | Lực chuẩn không rơi/bay cao |
| `DIFF` | index.html | Hệ số rơi & rung tay cho Dễ/Thường/Khó |

## Lưu ý
- **Chỉ chơi qua Wi-Fi:** laptop/TV và tất cả điện thoại phải cùng một mạng Wi-Fi (tắt 4G trên điện thoại). Kết nối P2P WebRTC qua PeerJS (signaling cần internet, dữ liệu chơi đi thẳng trong mạng LAN). Nếu router bật "AP/Client isolation" thì các máy không thấy nhau — hãy tắt tuỳ chọn đó.
- Rớt mạng: vào lại bằng cùng tên để nhận lại slot.
