# 🌌 Vũ trụ đơn giản

<img src="https://animations.sunflower-land.com/animated_webp/0_v1_32_1_5_15_46_41_23/idle-small" style="width: 52.5px;">

## Hi there! 👋 I'm nthun2k5

> Một mô hình vũ trụ thu nhỏ: Mặt Trời ở trung tâm, 3 hành tinh quay theo quỹ đạo tròn.  
> *Kéo chuột để xoay góc nhìn – không gian nhẹ nhàng, thư giãn.*

<!-- Nhúng canvas và script tạo vũ trụ -->
<canvas id="universeCanvas" width="900" height="600" style="display: block; margin: 0 auto; border-radius: 20px; box-shadow: 0 0 20px rgba(0,0,0,0.5); background: #000; cursor: grab;"></canvas>

<script>
  (function() {
    const canvas = document.getElementById('universeCanvas');
    const ctx = canvas.getContext('2d');
    let width = canvas.width = 900;
    let height = canvas.height = 600;

    // Điều khiển góc nhìn (kéo chuột)
    let cameraAngle = 0;
    let isDragging = false;
    let lastMouseX = 0;

    // Các thông số thiên thể
    const sun = { x: 0, y: 0, radius: 28, color: '#FDB813' };
    const planets = [
      { name: 'Sao Thủy', radius: 7, distance: 90, speed: 0.025, angle: 0, color: '#D2B48C', trail: [] },
      { name: 'Sao Kim',  radius: 9, distance: 130, speed: 0.015, angle: 1.8, color: '#E6B800', trail: [] },
      { name: 'Trái Đất', radius: 10, distance: 175, speed: 0.012, angle: 3.2, color: '#3B9EFF', trail: [] }
    ];
    
    // Sao nền
    const stars = [];
    for (let i = 0; i < 500; i++) {
      stars.push({
        x: Math.random() * width,
        y: Math.random() * height,
        radius: Math.random() * 2.2 + 0.8,
        alpha: Math.random() * 0.6 + 0.3,
        twinkle: Math.random() * 0.05
      });
    }

    // Vết đi của hành tinh (lưu tọa độ)
    for (let p of planets) {
      for (let i = 0; i < 40; i++) p.trail.push({ x: 0, y: 0 });
    }

    // Xử lý kéo chuột xoay vũ trụ
    canvas.addEventListener('mousedown', (e) => {
      isDragging = true;
      lastMouseX = e.clientX;
      canvas.style.cursor = 'grabbing';
    });
    window.addEventListener('mousemove', (e) => {
      if (!isDragging) return;
      const dx = e.clientX - lastMouseX;
      cameraAngle += dx * 0.008;
      lastMouseX = e.clientX;
    });
    window.addEventListener('mouseup', () => {
      isDragging = false;
      canvas.style.cursor = 'grab';
    });
    canvas.style.cursor = 'grab';

    // Hàm vẽ
    function draw() {
      ctx.clearRect(0, 0, width, height);
      
      // 1. Vẽ sao nền (lấp lánh nhẹ)
      for (let s of stars) {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255, 240, 200, ${s.alpha + Math.sin(Date.now() * s.twinkle) * 0.1})`;
        ctx.fill();
      }
      
      // 2. Bắt đầu transform xoay theo camera
      ctx.save();
      ctx.translate(width/2, height/2);
      ctx.rotate(cameraAngle);
      
      // 3. Quỹ đạo các hành tinh
      for (let p of planets) {
        ctx.beginPath();
        ctx.ellipse(0, 0, p.distance, p.distance, 0, 0, Math.PI * 2);
        ctx.strokeStyle = 'rgba(255,255,200,0.25)';
        ctx.lineWidth = 1.2;
        ctx.setLineDash([5, 8]);
        ctx.stroke();
      }
      ctx.setLineDash([]);
      
      // 4. Cập nhật góc & vị trí hành tinh
      for (let p of planets) {
        p.angle += p.speed;
        const x = Math.cos(p.angle) * p.distance;
        const y = Math.sin(p.angle) * p.distance;
        p.currentX = x;
        p.currentY = y;
        
        // Cập nhật vết đi (lưu lịch sử)
        p.trail.push({ x, y });
        if (p.trail.length > 45) p.trail.shift();
      }
      
      // 5. Vẽ vệt sáng của các hành tinh (hiệu ứng đuôi)
      for (let p of planets) {
        for (let i = 0; i < p.trail.length; i++) {
          const point = p.trail[i];
          const alpha = i / p.trail.length * 0.5;
          ctx.beginPath();
          ctx.arc(point.x, point.y, p.radius * 0.55, 0, Math.PI*2);
          ctx.fillStyle = `rgba(${hexToRgb(p.color)}, ${alpha + 0.1})`;
          ctx.fill();
        }
      }
      
      // 6. Vẽ các hành tinh
      for (let p of planets) {
        ctx.shadowBlur = 10;
        ctx.shadowColor = p.color;
        ctx.beginPath();
        ctx.arc(p.currentX, p.currentY, p.radius, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
        // Hiệu ứng viền sáng
        ctx.shadowBlur = 4;
        ctx.beginPath();
        ctx.arc(p.currentX, p.currentY, p.radius + 1.2, 0, Math.PI*2);
        ctx.strokeStyle = 'rgba(255,255,210,0.6)';
        ctx.lineWidth = 1;
        ctx.stroke();
      }
      
      // 7. Vẽ Mặt Trời (toả sáng)
      ctx.shadowBlur = 30;
      ctx.shadowColor = '#FDB813';
      ctx.beginPath();
      ctx.arc(0, 0, sun.radius, 0, Math.PI*2);
      ctx.fillStyle = sun.color;
      ctx.fill();
      // Hiệu ứng hào quang
      ctx.shadowBlur = 45;
      ctx.beginPath();
      ctx.arc(0, 0, sun.radius - 3, 0, Math.PI*2);
      ctx.fillStyle = '#FFAE42';
      ctx.fill();
      
      // Reset shadow
      ctx.shadowBlur = 0;
      
      // 8. Vẽ tên các hành tinh (chữ nhỏ)
      ctx.font = 'bold 12px "Segoe UI", system-ui';
      ctx.fillStyle = 'rgba(255,255,210,0.9)';
      ctx.shadowBlur = 0;
      for (let p of planets) {
        ctx.fillText(p.name, p.currentX + 12, p.currentY - 7);
      }
      ctx.fillStyle = '#FFE484';
      ctx.font = 'bold 14px monospace';
      ctx.fillText('🌞 Mặt Trời', 18, -12);
      
      ctx.restore(); // kết thúc transform camera
      
      // 9. Vẽ hướng dẫn góc phải
      ctx.font = '12px monospace';
      ctx.fillStyle = '#aaa';
      ctx.fillText('🖱️ Kéo chuột để xoay vũ trụ', width - 160, 30);
      
      requestAnimationFrame(draw);
    }
    
    // Helper chuyển màu hex -> rgb
    function hexToRgb(hex) {
      let r,g,b;
      if (hex.startsWith('#')) hex = hex.slice(1);
      if (hex.length === 6) {
        r = parseInt(hex.slice(0,2), 16);
        g = parseInt(hex.slice(2,4), 16);
        b = parseInt(hex.slice(4,6), 16);
      } else if (hex === 'D2B48C') { r=210,g=180,b=140; }
      else if (hex === 'E6B800') { r=230,g=184,b=0; }
      else if (hex === '3B9EFF') { r=59,g=158,b=255; }
      else return '200,200,200';
      return `${r},${g},${b}`;
    }
    
    draw();
  })();
</script>

---

## 🚀 About Me

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

---

## ✨ Giải thích về Vũ trụ

- **Mặt Trời** ở trung tâm, phát sáng.
- **3 hành tinh** (Sao Thủy, Sao Kim, Trái Đất) quay trên quỹ đạo với tốc độ khác nhau.
- **Hiệu ứng đuôi** mờ dần phía sau.
- **Kéo chuột ngang** để xoay góc nhìn toàn bộ vũ trụ.
- Hàng trăm **ngôi sao nền** lấp tinh nghịch.

> 💡 *Vì Markdown thuần không chạy script trên GitHub, bạn hãy mở file này bằng trình duyệt hoặc dùng Obsidian/Typora để thấy chuyển động.*  
> 🚀 Nếu bạn muốn nhúng vào GitHub README, hãy tạo một GitHub Pages hoặc dùng ảnh GIF thay thế.

--- 
**Nguyễn Thanh Hùng** – *Vũ trụ đơn giản dành cho người yêu không gian.* 🌠
