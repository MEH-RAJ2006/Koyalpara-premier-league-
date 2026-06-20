# Koyalpara-premier-league-
It's a football auction game 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elite PvP Auction League</title>
    <style>
        :root {
            --bg-stadium: #090c12;
            --panel-dark: #121824;
            --neon-green: #00ff87;
            --gold: #f5b041;
            --card-legend: linear-gradient(135deg, #2c1a4d 0%, #0f0720 100%);
            --card-modern: linear-gradient(135deg, #12284c 0%, #050f26 100%);
            --text-light: #f5f7fa;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', system-ui, sans-serif; }
        body { background-color: var(--bg-stadium); color: var(--text-light); padding: 15px; display: flex; justify-content: center; }
        .app-container { width: 100%; max-width: 480px; background: var(--panel-dark); border-radius: 20px; padding: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.7); border: 1px solid #1f2a3d; }
        h1 { font-size: 22px; text-align: center; color: var(--neon-green); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 20px; text-shadow: 0 0 10px rgba(0,255,135,0.2); }
        h2 { font-size: 15px; margin-bottom: 12px; color: #a0aec0; text-transform: uppercase; letter-spacing: 0.5px; }
        .hidden { display: none !important; }
        
        /* Interactive Input Fields */
        input, select { width: 100%; padding: 14px; background: #1a2233; border: 1px solid #2d3954; border-radius: 12px; color: #fff; font-size: 15px; margin-bottom: 15px; outline: none; transition: 0.2s; }
        input:focus, select:focus { border-color: var(--neon-green); box-shadow: 0 0 8px rgba(0,255,135,0.2); }
        .btn { width: 100%; padding: 14px; background: var(--neon-green); color: #000; font-weight: bold; border: none; border-radius: 12px; font-size: 16px; cursor: pointer; text-transform: uppercase; box-shadow: 0 4px 15px rgba(0,255,135,0.3); transition: 0.2s; }
        .btn:active { transform: scale(0.98); }
        .btn-add { background: transparent; border: 2px dashed var(--neon-green); color: var(--neon-green); margin-bottom: 15px; box-shadow: none; }
        
        /* Premium Football Card UI Layout */
        .fut-card { width: 210px; height: 300px; background: var(--card-legend); border: 3px solid var(--gold); border-radius: 16px; margin: 20px auto; position: relative; padding: 15px; box-shadow: 0 12px 30px rgba(0,0,0,0.7); overflow: hidden; }
        .fut-card.modern { background: var(--card-modern); border-color: var(--neon-green); }
        
        .card-meta { display: flex; flex-direction: column; position: absolute; top: 15px; left: 15px; align-items: center; line-height: 1; }
        .card-rating { font-size: 38px; font-weight: 900; color: var(--gold); }
        .fut-card.modern .card-rating { color: var(--neon-green); }
        .card-pos { font-size: 13px; font-weight: 800; color: #cbd5e1; text-transform: uppercase; margin-top: 2px; }
        
        .player-headshot { width: 130px; height: 130px; object-fit: contain; display: block; margin: 10px auto 0 auto; filter: drop-shadow(0 8px 10px rgba(0,0,0,0.5)); position: relative; z-index: 2; }
        
        .card-details { background: rgba(0,0,0,0.3); backdrop-filter: blur(5px); border-radius: 10px; padding: 8px 5px; margin-top: 15px; border: 1px solid rgba(255,255,255,0.05); text-align: center; position: relative; z-index: 3; }
        .player-name { font-weight: 800; font-size: 15px; color: #fff; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; text-transform: uppercase; }
        
        /* Flexbox Asset Badges Row */
        .badge-row { display: flex; justify-content: center; align-items: center; gap: 12px; margin-top: 6px; }
        .team-badge { width: 28px; height: 28px; object-fit: contain; }
        .flag-badge { width: 22px; height: 15px; object-fit: cover; border-radius: 2px; box-shadow: 0 2px 4px rgba(0,0,0,0.3); }
        
        /* Live Timer Dashboard Components */
        .timer-circle { width: 64px; height: 64px; border-radius: 50%; border: 4px solid #ff3b30; margin: 10px auto; display: flex; align-items: center; justify-content: center; font-size: 26px; font-weight: bold; color: #ff3b30; background: rgba(255,59,48,0.05); }
        .bid-status-banner { background: #1a2233; border-radius: 12px; padding: 14px; text-align: center; margin: 15px 0; font-weight: 600; border-left: 4px solid var(--neon-green); font-size: 14px; }
        .manager-row { display: flex; justify-content: space-between; align-items: center; background: #161e2e; padding: 12px 16px; border-radius: 12px; margin-bottom: 8px; border: 1px solid #232d42; }
        
        /* Final Table Structure Layout */
        table { width: 100%; border-collapse: collapse; margin-top: 15px; font-size: 14px; }
        th, td { padding: 12px 6px; text-align: center; }
        th { background: #1a2233; color: #a0aec0; font-weight: 600; text-transform: uppercase; font-size: 11px; }
        tr:nth-child(even) { background: #141b29; }
        .td-left { text-align: left; font-weight: bold; }
    </style>
</head>
<body>

<div class="app-container">
    <h1>🏆 PvP Auction League</h1>

    <div id="screen-setup">
        <h2>Register Group Managers (Max 8)</h2>
        <div id="input-container">
            <input type="text" placeholder="Manager 1 Name" class="mgr-input">
            <input type="text" placeholder="Manager 2 Name" class="mgr-input">
        </div>
        <button class="btn btn-add" onclick="addManagerField()">+ Add Room Space</button>
        <button class="btn" onclick="initiateTeamSelection()">Draft Club Specs</button>
    </div>

    <div id="screen-select" class="hidden">
        <h2 id="turn-indicator">Manager Selection Turn</h2>
        <select id="club-dropdown"></select>
        <select id="coach-dropdown"></select>
        <button class="btn" onclick="saveManagerChoices()">Confirm Selection</button>
    </div>

    <div id="screen-auction" class="hidden">
        <h2>Live Auction Block</h2>
        <div class="timer-circle" id="clock-display">10</div>
        
        <div id="active-card-target"></div>
        
        <div class="bid-status-banner" id="banner-text">Waiting for starting offer...</div>
        
        <select id="active-bidder-select"></select>
        <input type="number" id="bid-amount" placeholder="Enter bid value ($M)">
        <button class="btn" onclick="registerIncomingBid()" style="margin-bottom: 25px;">Submit Live Bid</button>
        
        <h2>Lobby Board Info</h2>
        <div id="lobby-stats-target"></div>
    </div>

    <div id="screen-tactics" class="hidden">
        <h2>Lock Team Strategy</h2>
        <div id="tactics-target"></div>
        <button class="btn" onclick="runTournamentMatchEngine()">Kickoff Champions League</button>
    </div>

    <div id="screen-results" class="hidden">
        <h2>League Points Standing Table</h2>
        <table>
            <thead>
                <tr>
                    <th style="text-align: left;">Team</th>
                    <th>W</th>
                    <th>D</th>
                    <th>L</th>
                    <th>GD</th>
                    <th>PTS</th>
                </tr>
            </thead>
            <tbody id="table-body-target"></tbody>
        </table>
        <div id="winner-banner" style="text-align: center; margin-top: 25px; font-weight: 900; font-size: 18px; color: var(--gold);"></div>
        <button class="btn" style="margin-top: 20px;" onclick="location.reload()">Reset Season Room</button>
    </div>
</div>

<script>
const CLUBS_POOL = ["Real Madrid", "Barcelona", "Man City", "Arsenal", "Bayern Munich", "Liverpool", "Juventus", "Inter Milan"];
const COACHES_POOL = {
    "Pep Guardiola": {att: 6, def: 2}, "Jose Mourinho": {att: 1, def: 7},
    "Carlo Ancelotti": {att: 4, def: 4}, "Sir Alex Ferguson": {att: 5, def: 4}
};
const SQUAD_FORMATIONS = ["4-3-3", "4-4-2", "3-5-2", "4-2-3-1"];

// Curated Elite Data Registry containing crisp Transparent Headshot portrait cuts and direct matching official badges
let playersPool = [
    {
        name: "Thomas Müller", legend: false, pos: "CAM", ovr: 86, 
        img: "https://cdn.sportmonks.com/images/soccer/players/11/523.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/6/67/FC_Bayern_M%C3%BCnchen_logo_%282017%29.svg",
        flag: "https://upload.wikimedia.org/wikipedia/en/b/ba/Flag_of_Germany.svg"
    },
    {
        name: "Cristiano Ronaldo", legend: false, pos: "ST", ovr: 93, 
        img: "https://images.footballdatabase.eu/player/642/642.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/en/4/47/Al-Nassr_FC_logo.svg",
        flag: "https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg"
    },
    {
        name: "Lionel Messi", legend: false, pos: "RW", ovr: 94, 
        img: "https://images.footballdatabase.eu/player/10499/10499.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/en/a/a4/Inter_Miami_CF_logo.svg",
        flag: "https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg"
    },
    {
        name: "Erling Haaland", legend: false, pos: "ST", ovr: 91, 
        img: "https://cdn.sportmonks.com/images/soccer/players/19/275.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/en/e/eb/Manchester_City_FC_badge.svg",
        flag: "https://upload.wikimedia.org/wikipedia/commons/d/d9/Flag_of_Norway.svg"
    },
    {
        name: "Kylian Mbappé", legend: false, pos: "LW", ovr: 92, 
        img: "https://images.footballdatabase.eu/player/279148/279148.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/5/56/Real_Madrid_CF.svg",
        flag: "https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg"
    },
    {
        name: "Pelé", legend: true, pos: "ST", ovr: 98, 
        img: "https://static.fifa.com/u/players/headshots/classic/178129.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/0/05/Flag_of_Brazil.svg",
        flag: "https://upload.wikimedia.org/wikipedia/commons/0/05/Flag_of_Brazil.svg"
    },
    {
        name: "Diego Maradona", legend: true, pos: "CAM", ovr: 97, 
        img: "https://static.fifa.com/u/players/headshots/classic/178103.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg",
        flag: "https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg"
    },
    {
        name: "Zinedine Zidane", legend: true, pos: "CM", ovr: 95, 
        img: "https://static.fifa.com/u/players/headshots/classic/178223.png", 
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/5/56/Real_Madrid_CF.svg",
        flag: "https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg"
    }
];

// Fallback background filling engine loops up to 350 to ensure zero loading crashes
while(playersPool.length < 350) {
    playersPool.push({
        name: `Elite Star Pro #${playersPool.length}`,
        legend: false,
        pos: ["ATT", "MID", "DEF", "GK"][Math.floor(Math.random()*4)],
        ovr: Math.floor(Math.random()*6)+82,
        img: "https://images.footballdatabase.eu/player/no-picture.png",
        teamImg: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/UEFA_Champions_League_logo_2.svg/1200px-UEFA_Champions_League_logo_2.svg.png",
        flag: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/UEFA_Champions_League_logo_2.svg/1200px-UEFA_Champions_League_logo_2.svg.png"
    });
}
playersPool.sort(() => Math.random() - 0.5);

let managers = [];
let turnIndex = 0;
let currentItem = null;
let topBid = 0;
let topBidder = null;
let clockVal = 10;
let loopTimer = null;

function addManagerField() {
    let div = document.getElementById("input-container");
    if(div.querySelectorAll("input").length < 8) {
        let el = document.createElement("input");
        el.type = "text";
        el.placeholder = `Manager ${div.querySelectorAll("input").length + 1} Name`;
        el.className = "mgr-input";
        div.appendChild(el);
    }
}

function initiateTeamSelection() {
    let inputs = document.querySelectorAll(".mgr-input");
    inputs.forEach(i => {
        let val = i.value.trim();
        if(val) managers.push({ name: val, club: "", coach: "", budget: 500, squad: [], formation: "", w:0, d:0, l:0, gf:0, ga:0, pts:0 });
    });
    if(managers.length < 2) { alert("Add at least 2 players."); managers = []; return; }
    
    document.getElementById("screen-setup").classList.add("hidden");
    document.getElementById("screen-select").classList.remove("hidden");
    
    let cSelect = document.getElementById("club-dropdown");
    let mSelect = document.getElementById("coach-dropdown");
    CLUBS_POOL.forEach(c => cSelect.add(new Option(c, c)));
    Object.keys(COACHES_POOL).forEach(co => mSelect.add(new Option(co, co)));
    
    runSelectionTracker();
}

function runSelectionTracker() {
    if(turnIndex >= managers.length) {
        document.getElementById("screen-select").classList.add("hidden");
        document.getElementById("screen-auction").classList.remove("hidden");
        runNextAuctionRound();
        return;
    }
    document.getElementById("turn-indicator").innerText = `${managers[turnIndex].name}'s Custom Setup Turn`;
}

function saveManagerChoices() {
    let cSel = document.getElementById("club-dropdown");
    let mSel = document.getElementById("coach-dropdown");
    
    managers[turnIndex].club = cSel.value;
    managers[turnIndex].coach = mSel.value;
    
    cSel.remove(cSel.selectedIndex);
    mSel.remove(mSel.selectedIndex);
    
    turnIndex++;
    runSelectionTracker();
}

function renderLobbyStatusGrid() {
    let target = document.getElementById("lobby-stats-target");
    let drop = document.getElementById("active-bidder-select");
    target.innerHTML = ""; drop.innerHTML = "";
    
    managers.forEach(m => {
        if(m.squad.length < 11) drop.add(new Option(m.name, m.name));
        target.innerHTML += `
            <div class="manager-row">
                <span><strong>${m.club}</strong> (${m.name})</span>
                <span>$${m.budget}M | ${m.squad.length}/11 slots</span>
            </div>
        `;
    });
}

function runNextAuctionRound() {
    renderLobbyStatusGrid();
    clearInterval(loopTimer);
    
    let activeList = managers.filter(m => m.squad.length < 11);
    if(activeList.length === 0 || playersPool.length === 0) {
        launchTacticsBoard();
        return;
    }
    
    currentItem = playersPool.shift();
    topBid = currentItem.legend ? 50 : 30;
    topBidder = null;
    
    document.getElementById("active-card-target").innerHTML = `
        <div class="fut-card ${!currentItem.legend ? 'modern' : ''}">
            <div class="card-meta">
                <div class="card-rating">${currentItem.ovr}</div>
                <div class="card-pos">${currentItem.pos}</div>
            </div>
            <img src="${currentItem.img}" class="player-headshot" onerror="this.src='https://images.footballdatabase.eu/player/no-picture.png'">
            <div class="card-details">
                <div class="player-name">${currentItem.name}</div>
                <div class="badge-row">
                    <img src="${currentItem.teamImg}" class="team-badge" alt="Club">
                    <img src="${currentItem.flag}" class="flag-badge" alt="Nation">
                </div>
            </div>
        </div>
    `;
    
    document.getElementById("banner-text").innerText = `Opening Ask Price: $${topBid}M`;
    clockVal = 10;
    document.getElementById("clock-display").innerText = clockVal;
    
    loopTimer = setInterval(() => {
        clockVal--;
        document.getElementById("clock-display").innerText = clockVal;
        if(clockVal <= 0) {
            clearInterval(loopTimer);
            finalizeCardOwner();
        }
    }, 1000);
}

function registerIncomingBid() {
    let name = document.getElementById("active-bidder-select").value;
    let amt = parseInt(document.getElementById("bid-amount").value);
    let m = managers.find(mgr => mgr.name === name);
    
    if(!amt || amt <= topBid) { alert("Bid must break current high threshold!"); return; }
    if(amt > m.budget) { alert("Insufficient funds room inside your budget bank!"); return; }
    
    topBid = amt;
    topBidder = m;
    document.getElementById("banner-text").innerText = `🔥 High Bid: $${topBid}M by ${m.name} (${m.club})`;
    clockVal = 10;
    document.getElementById("clock-display").innerText = clockVal;
}

function finalizeCardOwner() {
    if(topBidder) {
        topBidder.budget -= topBid;
        topBidder.squad.push(currentItem);
        alert(`🎉 SOLD! ${currentItem.name} officially signs with ${topBidder.club}!`);
    } else {
        alert(`❌ PASSED: ${currentItem.name} went unsold.`);
    }
    document.getElementById("bid-amount").value = "";
    runNextAuctionRound();
}

function launchTacticsBoard() {
    document.getElementById("screen-auction").classList.add("hidden");
    document.getElementById("screen-tactics").classList.remove("hidden");
    let target = document.getElementById("tactics-target");
    target.innerHTML = "";
    
    managers.forEach((m, idx) => {
        target.innerHTML += `
            <div style="background:#161e2e; padding:15px; border-radius:14px; margin-bottom:15px; border:1px solid #232d42;">
                <h3 style="color:var(--neon-green); margin-bottom:8px;">${m.club} (${m.name})</h3>
                <select id="strat-${idx}">
                    ${SQUAD_FORMATIONS.map(f => `<option value="${f}">${f}</option>`).join("")}
                </select>
            </div>
        `;
    });
}

function runTournamentMatchEngine() {
    managers.forEach((m, idx) => {
        m.formation = document.getElementById(`strat-${idx}`).value;
        let power = m.squad.reduce((s, p) => s + p.ovr, 0) / 11;
        m.att = power + COACHES_POOL[m.coach].att;
        m.def = power + COACHES_POOL[m.coach].def;
    });
    
    for(let i=0; i<managers.length; i++) {
        for(let j=i+1; j<managers.length; j++) {
            let mA = managers[i]; let mB = managers[j];
            let gfA = Math.max(0, Math.floor((mA.att - mB.def)/6 + Math.random()*4));
            let gfB = Math.max(0, Math.floor((mB.att - mA.def)/6 + Math.random()*4));
            
            mA.gf += gfA; mA.ga += gfB; mB.gf += gfB; mB.ga += gfA;
            if(gfA > gfB) { mA.pts += 3; mA.w++; mB.l++; }
            else if(gfB > gfA) { mB.pts += 3; mB.w++; mA.l++; }
            else { mA.pts += 1; mB.pts += 1; mA.d++; mB.d++; }
        }
    }
    
    document.getElementById("screen-tactics").classList.add("hidden");
    document.getElementById("screen-results").classList.remove("hidden");
    
    managers.sort((a,b) => b.pts - a.pts || (b.gf - b.ga) - (a.gf - a.ga));
    let body = document.getElementById("table-body-target");
    body.innerHTML = "";
    
    managers.forEach(m => {
        body.innerHTML += `
            <tr>
                <td class="td-left">${m.club}</td>
                <td>${m.w}</td>
                <td>${m.d}</td>
                <td>${m.l}</td>
                <td>${m.gf - m.ga}</td>
                <td><strong>${m.pts}</strong></td>
            </tr>
        `;
    });
    document.getElementById("winner-banner").innerText = `🏆 CHAMPION DEL MUNDO: ${managers[0].club.toUpperCase()} (${managers[0].name}) 🏆`;
}
</script>
</body>
</html>
