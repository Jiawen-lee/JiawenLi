---
layout: homepage
---

## Four Pillars of Destiny 四柱八字

I am an amateur of ancient Chinese fortune-telling - [Four Pillars](https://en.wikipedia.org/wiki/Four_Pillars_of_Destiny) (ba zi). It uses the date and time of your birth to infer your personality, relationship, and destiny based on the reactions and combinations of *Yin-yang* and *Wuxing* ([Five phases](https://en.wikipedia.org/wiki/Wuxing_(Chinese_philosophy))).

Feel free to contact me if you are interested in such things and I can tell about your future if possible. 

<img src="https://raw.githubusercontent.com/leeJiawen/blog-img/main/9cff50fa-1d86-4aad-a15b-1a8074671e3b.png" 
    style="display:block; margin: 0 auto; zoom:67%;" />

<hr>
<h3 style="text-align:center;">Calculate Your Four Pillars</h3>
<p style="text-align:center;">Enter your birth date, time and your gender:</p>

<div style="text-align:center;">
  <input type="datetime-local" id="birthInput" style="padding:6px; border-radius:6px; border:1px solid #ccc;">
  <select id="genderSelect" style="padding:8px 12px; border-radius:6px; border:1px solid #ccc; background-color:#fff; color:#333; cursor:pointer;">
    <option value="">Select</option>
    <option value="male">Male</option>
    <option value="female">Female</option>
    <option value="other">Other</option>
  </select>
  <button onclick="calcBazi()" style="margin-left:6px; padding:6px 12px; border:none; border-radius:6px; background:#2c3e50; color:white;">Calculate</button>
</div>

<div id="baziResult" style="
  margin-top:25px;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  gap:10px;
  font-size:1.2em;
  text-align:center;
  min-height:200px;
"></div>

<script src="https://cdn.jsdelivr.net/npm/lunar-javascript@1.6.12/lunar.min.js"></script>

<script>

function calcBazi() {
  const input = document.getElementById("birthInput").value;
  const gender = document.getElementById("genderSelect").value;
  if (!input) return alert("Please enter your birth date and time.");

  // Step 1: Gregorian date input
  const date = new Date(input);
  const year = date.getFullYear();
  const month = date.getMonth() + 1;
  const day = date.getDate();
  const hour = date.getHours();

  // Step 2: Convert to lunar using true algorithm
  const solar = Solar.fromYmdHms(year, month, day, hour, 0, 0);
  const lunar = solar.getLunar();

  // Step 3: Get true BaZi pillars
  const yearPillar  = lunar.getYearInGanZhiExact();   // 年柱
  const monthPillar = lunar.getMonthInGanZhiExact();  // 月柱
  const dayPillar   = lunar.getDayInGanZhiExact();    // 日柱
  const timePillar  = lunar.getTimeInGanZhi();        // 时柱

  console.log("True BaZi:", yearPillar, monthPillar, dayPillar, timePillar);

  // Step 4: Color + Pinyin map (for non-Chinese readers)
  const wuxingColors = {
    // Heavenly Stems (天干)
    "甲": { color: "#27ae60", pinyin: "Chia" },
    "乙": { color: "#27ae60", pinyin: "Yi" },
    "丙": { color: "#e74c3c", pinyin: "Ping" },
    "丁": { color: "#e74c3c", pinyin: "Ting" },
    "戊": { color: "#a57c1b", pinyin: "Wu" },
    "己": { color: "#a57c1b", pinyin: "Chi" },
    "庚": { color: "#d4ac0d", pinyin: "Keng" },
    "辛": { color: "#d4ac0d", pinyin: "Hsin" },
    "壬": { color: "#2980b9", pinyin: "Jen" },
    "癸": { color: "#2980b9", pinyin: "Kuei" },
    // 地支 Earthly Branches
    "子": { color: "#2980b9", pinyin: "Tzu" },
    "丑": { color: "#a57c1b", pinyin: "Ch'ou" },
    "寅": { color: "#27ae60", pinyin: "Yin" },
    "卯": { color: "#27ae60", pinyin: "Mao" },
    "辰": { color: "#a57c1b", pinyin: "Ch'en" },
    "巳": { color: "#e74c3c", pinyin: "Ssu" },
    "午": { color: "#e74c3c", pinyin: "Wu" },
    "未": { color: "#a57c1b", pinyin: "Wei" },
    "申": { color: "#d4ac0d", pinyin: "Shen" },
    "酉": { color: "#d4ac0d", pinyin: "Yo" },
    "戌": { color: "#a57c1b", pinyin: "Hsu" },
    "亥": { color: "#2980b9", pinyin: "Hai" }
  };

  const pillars = [
    { label: "Year 年柱",  text: yearPillar },
    { label: "Month 月柱", text: monthPillar },
    { label: "Day 日柱",   text: dayPillar },
    { label: "Hour 时柱",  text: timePillar }
  ];

  // Step 5: Render with Pinyin
  const html = `
    <div style="display:flex;justify-content:center;align-items:flex-end;gap:40px;margin-top:25px;">
      ${pillars.map(p => {
        const stem = p.text[0];
        const branch = p.text[1];
        const stemInfo = wuxingColors[stem];
        const branchInfo = wuxingColors[branch];
        return `
          <div style="display:flex;flex-direction:column;align-items:center;">
            <span style="margin-top:6px;font-size:0.9em;color:#555;">${p.label}</span>
            <span style="font-size:2em;font-weight:bold;color:${stemInfo.color};">
              ${stem} <span style="font-size:0.7em;color:#555;">${stemInfo.pinyin}</span>
            </span>
            <span style="font-size:2em;font-weight:bold;color:${branchInfo.color};">
              ${branch} <span style="font-size:0.7em;color:#555;">${branchInfo.pinyin}</span>
            </span>
          </div>
        `;
      }).join('')}
    </div>

    <p style="text-align:center;margin-top:12px;font-size:0.85em;color:#666;">
                <span style="color:#27ae60;">● Wood 木</span>　
                <span style="color:#e74c3c;">● Fire 火</span>　
                <span style="color:#a57c1b;">● Earth 土</span>　
                <span style="color:#d4ac0d;">● Metal 金</span>　
                <span style="color:#2980b9;">● Water 水</span>
</p>

<div style="display:flex; gap:12px; justify-content:center; margin-top:20px;">
  <button onclick="sendToGPT()" 
          style="background-color:#4A90E2; color:white; font-weight:500; padding:10px 22px; border:none; border-radius:6px; cursor:pointer; transition:0.2s; box-shadow:0 2px 4px rgba(0,0,0,0.1);">
    Ask GPT
  </button>

  <button onclick="sendEmail()" 
          style="background-color:#014687ff; color:white; font-weight:500; padding:10px 22px; border:none; border-radius:6px; cursor:pointer; transition:0.2s; box-shadow:0 2px 4px rgba(0,0,0,0.1);">
    Ask Master Li
  </button>
</div>

<div id="gptResponse" style="
     display:none;
     max-width:600px;
     margin:20px auto;
     padding:15px;
     border-radius:8px;
     background-color:#f9f9f9;
     color:#333;
     box-shadow:0 2px 6px rgba(0,0,0,0.05);
     font-size:0.95em;
     text-align: left;
"></div>
  `;

  document.getElementById("baziResult").innerHTML = html;

  return `${yearPillar} ${monthPillar} ${dayPillar} ${timePillar} ${gender}`;
}
async function sendToGPT() {
  const bazi = calcBazi();
  if (!bazi) return;

  const responseDiv = document.getElementById("gptResponse");
  responseDiv.style.display = "block";
  responseDiv.innerHTML = "Sending Bazi to GPT...";

  try {
    const response = await fetch("https://flask-python-boilerplate-wine.vercel.app/api/gpt", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ prompt: bazi })
    });

    if (!response.ok) throw new Error("Network response was not ok");

    const data = await response.json();

    // Render GPT response to the page
    responseDiv.innerHTML = `${data.response.replace(/\n/g, "<br>")}`;

  } catch (error) {
    console.error("Error sending Bazi to GPT:", error);
    responseDiv.innerHTML = "Failed to get GPT response. See console for details.";
  }
}

// Send via email
function sendEmail() {
  const bazi = calcBazi();
  if (!bazi) return;

  const email = "lijiawen@umich.edu";
  const subject = encodeURIComponent("My Bazi");
  const body = encodeURIComponent("Hello Master Li,\n\nHere is my Bazi:\n" + bazi);

  // Create a temporary link and click it
    const url = `https://mail.google.com/mail/?view=cm&fs=1&to=${email}&su=${subject}&body=${body}`;
    window.open(url, "_blank");
}

</script>
