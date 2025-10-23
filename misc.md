---
layout: homepage
---

## Four Pillars of Destiny 四柱八字

I am an amateur of ancient Chinese fortune-telling - [Four Pillars](https://en.wikipedia.org/wiki/Four_Pillars_of_Destiny) (ba zi). It uses the date and time of your birth to infer your personality, relationship, and destiny based on the reactions and combinations of *Yin-yang* and *Wuxing* ([Five phases](https://en.wikipedia.org/wiki/Wuxing_(Chinese_philosophy))).

Feel free to contact me if you are interested in such things and I can tell about your future if possible. 

<img src="https://raw.githubusercontent.com/leeJiawen/blog-img/main/9cff50fa-1d86-4aad-a15b-1a8074671e3b.png" 
    style="display:block; margin: 0 auto; zoom:67%;" />


<hr>
<h3>Calculate Your Four Pillars (生辰八字计算)</h3>
<p>Enter your birth date and time (Gregorian):</p>

<input type="datetime-local" id="birthInput" style="padding:6px; border-radius:6px; border:1px solid #ccc;">
<button onclick="calcBazi()" style="margin-left:6px; padding:6px 12px; border:none; border-radius:6px; background:#2c3e50; color:white;">Calculate</button>

<div id="baziResult" style="margin-top:15px; font-size:1.1em;"></div>

<script>
// === Basic 八字 calculator (approximate, for hobby/demo use) ===
// Converts Gregorian year/month/day/hour into Heavenly Stem + Earthly Branch

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

  // Year pillar
  const yearStemIndex = (year - 4) % 10;
  const yearBranchIndex = (year - 4) % 12;
  const yearPillar = stems[yearStemIndex] + " " + branches[yearBranchIndex];

  // Month pillar (simplified rule based on Spring Festival not accounted)
  const monthStemIndex = (yearStemIndex * 2 + month + 1) % 10;
  const monthBranchIndex = (month + 1) % 12;
  const monthPillar = stems[monthStemIndex] + " " + branches[monthBranchIndex];

  // Day pillar (approximation)
  const dayCount = Math.floor((date - new Date(year,0,0)) / (1000*60*60*24));
  const dayStemIndex = (dayCount + year * 5) % 10;
  const dayBranchIndex = (dayCount + year * 3) % 12;
  const dayPillar = stems[dayStemIndex] + " " + branches[dayBranchIndex];

  // Hour pillar
  const hourBranchIndex = Math.floor((hour + 1) / 2) % 12;
  const hourStemIndex = (dayStemIndex * 2 + hourBranchIndex) % 10;
  const hourPillar = stems[hourStemIndex] + " " + branches[hourBranchIndex];

  const result = `
    <b>Year Pillar:</b> ${yearPillar}<br>
    <b>Month Pillar:</b> ${monthPillar}<br>
    <b>Day Pillar:</b> ${dayPillar}<br>
    <b>Hour Pillar:</b> ${hourPillar}
  `;
  document.getElementById("baziResult").innerHTML = result;
}
</script>