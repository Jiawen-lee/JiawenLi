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
<p style="text-align:center;">Enter your birth date and time:</p>

<div style="text-align:center;">
  <input type="datetime-local" id="birthInput" style="padding:6px; border-radius:6px; border:1px solid #ccc;">
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
<script>
    
function calcBazi() {
  const input = document.getElementById("birthInput").value;
  if (!input) return alert("Please enter your birth date and time.");

  const date = new Date(input);
  const year = date.getFullYear();
  const month = date.getMonth() + 1;
  const day = date.getDate();
  const hour = date.getHours();

  const stems = ["Jia 甲","Yi 乙","Bing 丙","Ding 丁","Wu 戊","Ji 己","Geng 庚","Xin 辛","Ren 壬","Gui 癸"];
  const branches = ["Zi 子","Chou 丑","Yin 寅","Mao 卯","Chen 辰","Si 巳","Wu 午","Wei 未","Shen 申","You 酉","Xu 戌","Hai 亥"];

  // === Pillar calculation ===
  const yearStemIndex = (year - 4) % 10;
  const yearBranchIndex = (year - 4) % 12;
  const monthStemIndex = (yearStemIndex * 2 + month + 1) % 10;
  const monthBranchIndex = (month + 1) % 12;
  const dayCount = Math.floor((date - new Date(year,0,0)) / (1000*60*60*24));
  const dayStemIndex = (dayCount + year * 5) % 10;
  const dayBranchIndex = (dayCount + year * 3) % 12;
  const hourBranchIndex = Math.floor((hour + 1) / 2) % 12;
  const hourStemIndex = (dayStemIndex * 2 + hourBranchIndex) % 10;

  // === Wuxing color map ===
  const wuxingColors = {
    // Heavenly Stems
    "Jia 甲": "#27ae60", "Yi 乙": "#27ae60",         // Wood
    "Bing 丙": "#e74c3c", "Ding 丁": "#e74c3c",       // Fire
    "Wu 戊": "#a57c1b", "Ji 己": "#a57c1b",           // Earth
    "Geng 庚": "#d4ac0d", "Xin 辛": "#d4ac0d",       // Metal
    "Ren 壬": "#2980b9", "Gui 癸": "#2980b9",         // Water
    // Earthly Branches
    "Zi 子": "#2980b9", "Chou 丑": "#a57c1b", "Yin 寅": "#27ae60", "Mao 卯": "#27ae60",
    "Chen 辰": "#a57c1b", "Si 巳": "#e74c3c", "Wu 午": "#e74c3c", "Wei 未": "#a57c1b",
    "Shen 申": "#d4ac0d", "You 酉": "#d4ac0d", "Xu 戌": "#a57c1b", "Hai 亥": "#2980b9"
  };

  // === Pillar objects ===
  const pillars = [
    { label: "Year", stem: stems[yearStemIndex], branch: branches[yearBranchIndex] },
    { label: "Month", stem: stems[monthStemIndex], branch: branches[monthBranchIndex] },
    { label: "Day", stem: stems[dayStemIndex], branch: branches[dayBranchIndex] },
    { label: "Hour", stem: stems[hourStemIndex], branch: branches[hourBranchIndex] }
  ];

  // === Render horizontally aligned Four Pillars ===
  const html = `
    <div style="
      display: flex;
      justify-content: center;
      align-items: flex-end;
      gap: 40px;
      margin-top: 25px;
    ">
      ${pillars.map(p => `
        <div style="display: flex; flex-direction: column; align-items: center;">
          <span style="font-size: 2em; font-weight: bold; color:${wuxingColors[p.stem]}; line-height: 1.1;">
            ${p.stem.split(' ')[1]}
          </span>
          <span style="font-size: 2em; font-weight: bold; color:${wuxingColors[p.branch]}; line-height: 1.1;">
            ${p.branch.split(' ')[1]}
          </span>
          <span style="margin-top:6px; font-size: 0.9em; color:#555;">${p.label}</span>
        </div>
      `).join('')}
    </div>
  `;

  document.getElementById("baziResult").innerHTML = html;
}
</script>
