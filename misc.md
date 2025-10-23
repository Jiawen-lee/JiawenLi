---
layout: homepage
---

## Four Pillars of Destiny 四柱八字

I am an amateur of ancient Chinese fortune-telling - [Four Pillars](https://en.wikipedia.org/wiki/Four_Pillars_of_Destiny) (ba zi). It uses the date and time of your birth to infer your personality, relationship, and destiny based on the reactions and combinations of *Yin-yang* and *Wuxing* ([Five phases](https://en.wikipedia.org/wiki/Wuxing_(Chinese_philosophy))).

Feel free to contact me if you are interested in such things and I can tell about your future if possible. 

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

{% raw %}
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

  const yearStemIndex = (year - 4) % 10;
  const yearBranchIndex = (year - 4) % 12;
  const yearPillar = stems[yearStemIndex] + " " + branches[yearBranchIndex];

  const monthStemIndex = (yearStemIndex * 2 + month + 1) % 10;
  const monthBranchIndex = (month + 1) % 12;
  const monthPillar = stems[monthStemIndex] + " " + branches[monthBranchIndex];

  const dayCount = Math.floor((date - new Date(year,0,0)) / (1000*60*60*24));
  const dayStemIndex = (dayCount + year * 5) % 10;
  const dayBranchIndex = (dayCount + year * 3) % 12;
  const dayPillar = stems[dayStemIndex] + " " + branches[dayBranchIndex];

  const hourBranchIndex = Math.floor((hour + 1) / 2) % 12;
  const hourStemIndex = (dayStemIndex * 2 + hourBranchIndex) % 10;
  const hourPillar = stems[hourStemIndex] + " " + branches[hourBranchIndex];

  const wuxingColors = {
    "Jia 甲": "#27ae60", // Wood
    "Yi 乙": "#27ae60", // Wood
    "Bing 丙": "#c0392b", // Fire
    "Ding 丁": "#c0392b", // Fire
    "Wu 戊": "#716121ff", // Earth
    "Ji 己": "#716121ff", // Earth
    "Geng 庚": "#dcbf00ff", // Metal
    "Xin 辛": "#dcbf00ff", // Metal
    "Ren 壬": "#2980b9", // Water
    "Gui 癸": "#2980b9"  // Water
    "Zi 子":"#2980b9",
    "Chou 丑":"#716121ff",
    "Yin 寅":"#27ae60",
    "Mao 卯":"#27ae60",
    "Chen 辰":"#716121ff",
    "Si 巳":"#c0392b",
    "Wu 午":"#c0392b",
    "Wei 未":"#716121ff",
    "Shen 申":"#dcbf00ff",
    "You 酉":"#dcbf00ff",
    "Xu 戌":"#716121ff",
    "Hai 亥":"#2980b9"
  };

  const pillars = [
    { label: "Year", value: yearPillar, color: wuxingColors[stems[yearStemIndex]] },
    { label: "Month", value: monthPillar, color: wuxingColors[stems[monthStemIndex]] },
    { label: "Day", value: dayPillar, color: wuxingColors[stems[dayStemIndex]] },
    { label: "Hour", value: hourPillar, color: wuxingColors[stems[hourStemIndex]] }
  ];

  const html = pillars.map(p => `
    <div style="color:${p.color}; font-weight:bold; display:flex; flex-direction:column; align-items:center;">
      <span style="font-size:0.9em; color:#555;">${p.label} Pillar</span>
      <span style="font-size:1.3em;">${p.value}</span>
    </div>
  `).join("");

  document.getElementById("baziResult").innerHTML = html;
}
</script>
{% endraw %}