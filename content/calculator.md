---
title: "Kenya Solar Size Calculator (2026)"
description: "Stop guessing! Use John's free solar calculator to find out exactly what size Must, Growatt, or Deye inverter you need based on your KPLC bill."
layout: "page"
url: "/calculator/"
---

# The "No-Nonsense" Solar Calculator 🇰🇪

<div style="display: flex; align-items: center; gap: 15px; margin-bottom: 25px; background: #f8f9fa; padding: 15px; border-left: 5px solid #f39c12; border-radius: 4px;">
  <p style="margin: 0; font-size: 16px; line-height: 1.6;"><strong>Hi, I'm John.</strong> I used to spend my weekends looking under car hoods, making sure mechanics weren't overcharging me for parts I didn't need. Now, I do the same thing for solar. <br><br>Don't let a salesman sell you a V8 engine when you only need a Toyota Vitz. Tell me your KPLC bill, and I'll tell you the exact system size you need to beat the blackouts.</p>
</div>

### Step 1: Tell me about your power usage

<div style="background: #ffffff; padding: 30px; border-radius: 12px; border: 1px solid #e5e7eb; box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1); margin: 20px 0;">
  
  <label style="font-weight: bold; display: block; margin-bottom: 8px; color: #374151;">1. What is your average monthly KPLC bill? (KES)</label>
  <input type="number" id="kplcBill" placeholder="e.g., 4500" style="width: 100%; padding: 12px; border-radius: 6px; border: 1px solid #d1d5db; font-size: 16px; margin-bottom: 20px; box-sizing: border-box;">

  <label style="font-weight: bold; display: block; margin-bottom: 8px; color: #374151;">2. What is your main goal for buying solar?</label>
  <select id="userGoal" style="width: 100%; padding: 12px; border-radius: 6px; border: 1px solid #d1d5db; font-size: 16px; margin-bottom: 25px; background-color: white; box-sizing: border-box;">
    <option value="basic">Just survive blackouts (Lights, TV, WiFi, Laptops)</option>
    <option value="standard">Keep the house running (Add Fridge & Microwave)</option>
    <option value="heavy">Total Independence (Add Water Pump / Iron Box / Heavy AC)</option>
  </select>
  
 <button id="analyzeBtn" style="width: 100%; background: #f39c12; color: white; border: none; padding: 16px; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 18px; transition: background 0.3s;">Analyze My Needs ⚡</button>
  <div id="resultsBox" style="display: none; margin-top: 30px; padding-top: 25px; border-top: 2px dashed #e5e7eb;">
    <h3 style="margin-top: 0; color: #111827; font-size: 22px;">John's Diagnostic Report:</h3>
    
    <div style="background: #fdf2e9; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
      <p style="margin: 0 0 10px 0; font-size: 18px;"><strong style="color: #d35400;">Inverter Size:</strong> <span id="resInverter"></span></p>
      <p style="margin: 0 0 10px 0; font-size: 18px;"><strong style="color: #d35400;">Battery Bank:</strong> <span id="resBattery"></span></p>
      <p style="margin: 0; font-size: 18px;"><strong style="color: #d35400;">The "Car Guy" Verdict:</strong> <span id="resVerdict" style="font-style: italic;"></span></p>
    </div>

    <p style="font-size: 15px; color: #4b5563; line-height: 1.5;">This is a rough estimate to protect you from being oversold. To get actual prices for trusted brands like <strong>Must</strong> or <strong>Growatt</strong> from platforms like Jumia, send these results directly to my WhatsApp. I'll review it for free!</p>

    <a id="whatsappBtn" href="#" target="_blank" style="display: block; text-align: center; width: 100%; background: #25D366; color: white; text-decoration: none; padding: 16px; border-radius: 8px; font-weight: bold; font-size: 18px; margin-top: 15px; box-sizing: border-box;">📲 Send this to John on WhatsApp</a>
  </div>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const btn = document.getElementById('analyzeBtn');
    
    if(btn) {
        btn.addEventListener('click', function(e) {
            e.preventDefault(); // Prevents the page from refreshing
            
            const billInput = document.getElementById('kplcBill').value;
            const bill = parseInt(billInput);
            const goal = document.getElementById('userGoal').value;
            
            if (!bill || bill <= 0 || isNaN(bill)) {
                alert("Please enter a valid KPLC bill amount (e.g., 4500).");
                return;
            }

            let inverter, battery, verdict;

            // Logic Tree
            if (goal === "basic" || bill < 3000) {
                inverter = "1kW - 3kW (e.g., Must PV1800)";
                battery = "100Ah / 12V Gel or 24V Lithium";
                verdict = "This is the 'Toyota Vitz' setup. It's affordable, highly reliable for daily small loads, and will keep you online when KPLC drops out. Don't let anyone sell you a 5kW system for this!";
            } else if (goal === "standard" || (bill >= 3000 && bill <= 10000)) {
                inverter = "5kW (e.g., Growatt SPF 5000)";
                battery = "5kWh Lithium (e.g., Felicity or Pylontech)";
                verdict = "This is the 'Toyota Fielder' setup. It's the most popular system in Nairobi right now. It comfortably runs your fridge and lights, and the Lithium battery will last you 10+ years without maintenance.";
            } else {
                inverter = "8kW+ Hybrid (e.g., Deye or Sunsynk)";
                battery = "10kWh+ Lithium";
                verdict = "This is the 'Land Cruiser' setup. You are running heavy machinery or large pumps. You need a premium inverter that can handle massive power surges without tripping.";
            }

            // Update the text on the page
            document.getElementById('resInverter').innerText = inverter;
            document.getElementById('resBattery').innerText = battery;
            document.getElementById('resVerdict').innerText = verdict;
            
            // Generate the WhatsApp Link
            const phone = "254748101279";
            const rawMessage = "Hi John! 👋 I just used your Solar Calculator on the website.\n\nMy KPLC Bill: " + bill + " KES\nMy Goal: " + goal + "\nYour Tool Suggested: A " + inverter + " with a " + battery + " battery.\n\nCan you help me find the best Jumia links or deals for this setup?";
            const encodedMessage = encodeURIComponent(rawMessage);
            document.getElementById('whatsappBtn').href = "https://wa.me/" + phone + "?text=" + encodedMessage;

            // Reveal the hidden results box
            document.getElementById('resultsBox').style.display = 'block';
        });
    }
});
</script>

---

### Why I built this tool
Most installers in Nairobi will look at your house size, not your actual power usage. If you have a 4-bedroom house but you only watch TV and use a laptop, you do **not** need a 10kW system. 

I do the research so you don't have to. Once we confirm your size on WhatsApp, I can point you toward the most reliable verified sellers on Jumia, ensuring you get warranties that actually work.
