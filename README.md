<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UTHC Ulluriaq — Scheduling App Prototype</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg0:#f0ede7;--bg1:#f7f6f2;--bg2:#fff;--bd:#ddd9d0;--bd2:#c8c4bb;
  --t1:#2b2a27;--t2:#6b6962;--t3:#9a978d;
  --blue:#185FA5;--bluedark:#0C447C;--bluelight:#E6F1FB;--bluemid:#B5D4F4;
  --green:#27500A;--greenlight:#EAF3DE;--greenmid:#97C459;
  --amber:#633806;--amberlight:#FAEEDA;
  --red:#791F1F;--redlight:#FCEBEB;
  --teal:#085041;--teallight:#E1F5EE;
  --pink:#72243E;--pinklight:#FBEAF0;
  --purple:#5B2196;--purplelight:#F3E8FF;
  --r:8px;--rl:14px;
}
body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;color:var(--t1);background:var(--bg0);font-size:13px;min-height:100vh}

/* NAV */
.topnav{display:flex;align-items:center;gap:0;background:var(--bg2);border-bottom:1px solid var(--bd);padding:0;overflow-x:auto;position:sticky;top:0;z-index:100}
.nav-logo{padding:12px 18px;font-size:13px;font-weight:600;color:var(--blue);white-space:nowrap;border-right:1px solid var(--bd)}
.nav-item{padding:12px 14px;font-size:12px;font-weight:500;color:var(--t2);cursor:pointer;border-bottom:3px solid transparent;white-space:nowrap}
.nav-item:hover{color:var(--t1);background:var(--bg1)}
.nav-item.on{color:var(--blue);border-bottom-color:var(--blue)}
.nav-badge{font-size:9px;background:#E24B4A;color:#fff;border-radius:8px;padding:1px 5px;margin-left:3px;font-weight:600}
.nav-right{margin-left:auto;padding:8px 14px;display:flex;align-items:center;gap:8px;border-left:1px solid var(--bd)}
.role-label{font-size:11px;color:var(--t3)}
.role-switch{padding:5px 12px;border-radius:var(--r);border:1px solid var(--bd2);font-size:11px;cursor:pointer;font-weight:500;background:var(--bg2);color:var(--t2)}
.role-switch:hover{background:var(--bg1)}

/* MAIN */
.main{max-width:1100px;margin:0 auto;padding:1.25rem}
.page{display:none}.page.on{display:block}

/* CARDS */
.card{background:var(--bg2);border:1px solid var(--bd);border-radius:var(--rl);padding:1rem 1.1rem;margin-bottom:.9rem}
.card-title{font-size:13px;font-weight:600;margin-bottom:.7rem;display:flex;justify-content:space-between;align-items:center}
.grid2{display:grid;grid-template-columns:1.4fr 1fr;gap:.9rem;margin-bottom:.9rem}
@media(max-width:600px){.grid2{grid-template-columns:1fr}}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:.9rem}
@media(max-width:500px){.grid4{grid-template-columns:repeat(2,1fr)}}
.stat{background:var(--bg1);border-radius:var(--r);padding:.8rem;text-align:center}
.stat-n{font-size:22px;font-weight:600;margin-bottom:2px}
.stat-l{font-size:10px;color:var(--t2)}

/* TABLES */
table.bt{width:100%;border-collapse:collapse;font-size:12px}
table.bt th{text-align:left;padding:6px 8px;font-size:11px;font-weight:600;color:var(--t2);background:var(--bg1);border-bottom:1px solid var(--bd)}
table.bt td{padding:7px 8px;border-bottom:1px solid var(--bd);vertical-align:middle}
table.bt tr:last-child td{border-bottom:none}

/* BUTTONS */
.btn{padding:7px 16px;border-radius:var(--r);border:1px solid var(--bd2);background:var(--bg2);font-size:12px;font-weight:500;cursor:pointer;color:var(--t1)}
.btn:hover{background:var(--bg1)}
.btn.pri{background:var(--blue);color:#fff;border-color:var(--blue)}
.btn.pri:hover{background:var(--bluedark)}
.btn.grn{background:var(--greenlight);color:var(--green);border-color:var(--greenmid)}
.btn.amb{background:var(--amberlight);color:var(--amber);border-color:#EF9F27}
.btn.red{background:var(--redlight);color:var(--red);border-color:#F09595}
.btn.sm{padding:4px 10px;font-size:11px}

/* BADGES */
.badge{font-size:10px;padding:2px 8px;border-radius:4px;font-weight:600}
.b-act{background:var(--greenlight);color:var(--green)}
.b-sus{background:var(--amberlight);color:var(--amber)}
.b-ter{background:var(--redlight);color:var(--red)}
.b-mat{background:var(--pinklight);color:var(--pink)}
.b-cnesst{background:var(--amberlight);color:var(--amber)}
.b-sick{background:var(--redlight);color:var(--red)}
.b-vac{background:var(--greenlight);color:var(--green)}
.b-ft{background:var(--bluelight);color:var(--blue)}

/* INFO / WARN */
.info{background:var(--bluelight);color:var(--bluedark);border:1px solid var(--bluemid);border-radius:var(--r);padding:9px 12px;font-size:12px;margin-bottom:.8rem;line-height:1.5}
.lock-pill{font-size:10px;background:var(--bluelight);color:var(--bluedark);border-radius:8px;padding:2px 8px;font-weight:600}

/* FIELD */
.field{margin-bottom:.9rem}
.field label{display:block;font-size:11px;font-weight:600;color:var(--t2);margin-bottom:5px}
.field input,.field select,.field textarea{width:100%;padding:8px 10px;border-radius:var(--r);border:1px solid var(--bd2);font-size:12px;background:var(--bg2);color:var(--t1)}

/* LOGIN */
.login-wrap{min-height:calc(100vh - 50px);display:flex;align-items:center;justify-content:center;padding:2rem}
.login-card{background:var(--bg2);border:1px solid var(--bd);border-radius:var(--rl);padding:2rem;width:360px;max-width:100%}
.login-logo{display:flex;align-items:center;gap:12px;margin-bottom:1.75rem}
.login-mark{width:42px;height:42px;border-radius:var(--r);background:var(--bluelight);display:flex;align-items:center;justify-content:center;font-size:22px}
.login-title{font-size:16px;font-weight:600}
.login-sub{font-size:11px;color:var(--t3)}
.role-seg{display:flex;background:var(--bg1);border-radius:var(--r);padding:3px;margin-bottom:1.5rem}
.role-opt{flex:1;text-align:center;padding:8px 0;font-size:12px;font-weight:500;border-radius:6px;cursor:pointer;color:var(--t2)}
.role-opt.on{background:var(--bg2);color:var(--blue);box-shadow:0 0 0 1px var(--bd)}
.otp-note{background:var(--bluelight);border-radius:var(--r);padding:10px 12px;font-size:11px;color:var(--bluedark);margin-top:1rem;line-height:1.5}
.login-link{font-size:11px;color:var(--t3);text-align:center;margin-top:.85rem}
.login-link a{color:var(--blue);cursor:pointer}

/* SCHED GRID */
.sched-tabs{display:flex;gap:2px;border-bottom:1px solid var(--bd);margin-bottom:1rem;overflow-x:auto}
.st{padding:8px 13px;font-size:12px;font-weight:500;color:var(--t2);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;display:flex;align-items:center;gap:5px}
.st.on{color:var(--blue);border-bottom-color:var(--blue)}
.pin{font-size:11px;color:var(--t3);cursor:pointer}
.pin.hp{color:var(--blue)}
.home-banner{background:var(--bluelight);color:var(--bluedark);border-radius:var(--r);padding:8px 11px;font-size:12px;margin-bottom:.8rem;display:flex;align-items:center;gap:7px}
.sched-panel{display:none}.sched-panel.on{display:block}
.sched-scroll{overflow-x:auto}
.wk-label{font-size:10px;font-weight:700;color:var(--blue);text-transform:uppercase;letter-spacing:.04em;padding:7px 4px 4px;background:var(--bg2);position:sticky;top:0;z-index:4}
.wk-label.pp2{color:var(--pink)}
table.sg{border-collapse:collapse;font-size:10px;min-width:100%;margin-bottom:.4rem}
table.sg th,table.sg td{border:1px solid var(--bd)}
table.sg th{background:var(--bg1);font-weight:600;font-size:9px;color:var(--t2);text-align:center;padding:3px 1px}
th.nh{text-align:left;padding:3px 7px;width:110px;min-width:110px;max-width:110px;background:var(--bg1)}
td.nh{text-align:left;padding:3px 7px;width:110px;min-width:110px;max-width:110px;font-weight:600;background:var(--bg2);font-size:10px;overflow:hidden}
td.nm{white-space:nowrap;overflow:hidden;text-overflow:ellipsis;display:block}
td.mt{font-size:8px;color:var(--t3);font-weight:400;display:block}
td.std{width:46px;min-width:46px;padding:1px;text-align:center}
.cell{display:flex;flex-direction:column;align-items:center;justify-content:center;border-radius:3px;font-size:10px;font-weight:700;min-height:22px;padding:2px 3px;line-height:1.2;width:100%;box-sizing:border-box}
.cell-main{font-size:11px;font-weight:800;letter-spacing:.3px}
.J1{background:#1e40af;color:#fff}
.J2{background:#2563EB;color:#fff}
.S1{background:#B45309;color:#fff}
.S2{background:#D97706;color:#fff}
.N{background:#4C1D95;color:#fff}
.OT{background:#0C447C;color:#fff}
.TRAN{background:#374151;color:#fff;cursor:pointer}
.ESC{background:#064E3B;color:#fff;cursor:pointer}
.R{background:#e5e7eb;color:#6b7280}
.V{background:#15803D;color:#fff}
.em{background:var(--bg1);color:var(--t3);font-weight:400}
.mine td.nh{background:#FFFCE8}
.cover{font-size:7px;font-style:italic;opacity:.9}
.legend{display:flex;flex-wrap:wrap;gap:6px;padding:.5rem 0;font-size:10px}
.lgi{display:flex;align-items:center;gap:4px}
.lgd{width:18px;height:12px;border-radius:2px;font-size:8px;display:flex;align-items:center;justify-content:center;font-weight:600}

/* MESSAGING */
.msg-app{display:flex;border:1px solid var(--bd);border-radius:var(--rl);overflow:hidden;height:420px;background:var(--bg2)}
.msg-sb{width:210px;min-width:210px;border-right:1px solid var(--bd);display:flex;flex-direction:column;overflow-y:auto}
.msg-sb-head{padding:.7rem .9rem;border-bottom:1px solid var(--bd);font-size:12px;font-weight:600}
.conv{display:flex;gap:8px;padding:9px .9rem;cursor:pointer;border-bottom:1px solid var(--bd)}
.conv:hover{background:var(--bg1)}
.conv.on{background:var(--bluelight)}
.av{width:30px;height:30px;border-radius:50%;background:var(--greenlight);color:var(--green);font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.cv-name{font-size:11px;font-weight:600}
.cv-prev{font-size:10px;color:var(--t2)}
.msg-main{flex:1;display:flex;flex-direction:column;overflow:hidden}
.msg-head{padding:.7rem .9rem;border-bottom:1px solid var(--bd);font-weight:600;font-size:13px}
.msg-body{flex:1;overflow-y:auto;padding:.9rem;display:flex;flex-direction:column;gap:8px}
.bub{max-width:75%;padding:8px 11px;border-radius:10px;font-size:12px;line-height:1.4}
.bub.them{background:var(--bg1);align-self:flex-start}
.bub.me{background:var(--blue);color:#fff;align-self:flex-end}
.sw-card{align-self:center;width:92%;background:var(--bg2);border:1px solid #85B7EB;border-radius:var(--rl);padding:.85rem;font-size:12px}
.sw-title{font-weight:600;margin-bottom:.5rem;color:var(--bluedark);display:flex;align-items:center;gap:6px}
.sw-row{display:flex;justify-content:space-between;padding:4px 0;border-bottom:1px solid var(--bd);font-size:12px}
.sw-row:last-of-type{border-bottom:none}
.sw-status{display:flex;gap:5px;flex-wrap:wrap;margin-top:.6rem}
.pill{font-size:10px;padding:3px 9px;border-radius:9px;font-weight:600}
.pill.done{background:var(--greenlight);color:var(--green)}
.pill.wait{background:var(--amberlight);color:var(--amber)}
.pill.pend{background:var(--bg1);color:var(--t3)}
.msg-input{display:flex;gap:6px;padding:.7rem;border-top:1px solid var(--bd)}
.msg-input input{flex:1;padding:7px 10px;border-radius:var(--r);border:1px solid var(--bd2);font-size:12px}
.sw-trigger{padding:5px 11px;border-radius:var(--r);border:1px dashed var(--bd2);font-size:11px;cursor:pointer;color:var(--t2);background:var(--bg1);white-space:nowrap}
.sw-trigger:hover{background:var(--bluelight);color:var(--blue)}

/* SENIORITY */
.sen-list{list-style:none}
.sen-row{display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--bg2);border:1px solid var(--bd);border-radius:var(--r);margin-bottom:5px;cursor:grab}
.sen-row.dragging{opacity:.35}
.sen-rank{width:26px;height:26px;border-radius:50%;background:var(--bluelight);color:var(--bluedark);font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.sen-name{font-weight:500;flex:1;font-size:12px}
.sen-meta{font-size:11px;color:var(--t2)}
.arr{width:22px;height:22px;border-radius:5px;border:1px solid var(--bd);background:var(--bg2);cursor:pointer;font-size:13px}
.arr:hover{background:var(--bg1)}
.arr:disabled{opacity:.3;cursor:default}

/* MODAL */
.modal-wrap{display:none;position:fixed;inset:0;background:rgba(0,0,0,.4);align-items:center;justify-content:center;z-index:200}
.modal-wrap.open{display:flex}
.modal{background:var(--bg2);border:1px solid var(--bd);border-radius:var(--rl);padding:1.25rem;width:400px;max-width:94%;max-height:90vh;overflow-y:auto}
.modal-title{font-size:14px;font-weight:600;margin-bottom:.85rem;display:flex;justify-content:space-between;align-items:center}
.mx{cursor:pointer;color:var(--t3);font-size:20px;line-height:1}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:.65rem}
.deny-screen{text-align:center;padding:2.5rem 1rem}
.deny-icon{font-size:36px;margin-bottom:.65rem;color:var(--red)}

/* DEPT BAR */
.dep-row{display:flex;align-items:center;justify-content:space-between;padding:6px 0;border-bottom:1px solid var(--bd);font-size:12px}
.dep-row:last-child{border-bottom:none}
.bar-bg{flex:1;height:5px;background:var(--bg1);border-radius:3px;margin:0 8px}
.bar-fill{height:100%;border-radius:3px;background:var(--blue)}

/* LTABS */
.ltabs{display:flex;flex-wrap:wrap;gap:5px;margin-top:5px}
.ltab{padding:5px 12px;border-radius:var(--r);border:1px solid var(--bd);font-size:11px;cursor:pointer;background:var(--bg2);color:var(--t2)}
.ltab.on{background:var(--bluelight);color:var(--bluedark);border-color:#85B7EB;font-weight:600}

/* MEMO */
.memo-card{background:var(--bg2);border:1px solid var(--bd);border-radius:var(--rl);padding:.95rem;margin-bottom:.75rem}
.memo-type{display:inline-flex;align-items:center;gap:4px;font-size:10px;padding:3px 9px;border-radius:9px;font-weight:600;margin-bottom:.5rem}
.mt-escort{background:var(--teallight);color:var(--teal)}
.mt-transport{background:var(--bluelight);color:var(--bluedark)}
.memo-title{font-size:13px;font-weight:600;margin-bottom:.5rem}
.memo-grid{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:.5rem}
.memo-field{background:var(--bg1);border-radius:var(--r);padding:7px 9px}
.memo-label{font-size:9px;color:var(--t2);margin-bottom:2px}
.memo-val{font-weight:600;font-size:12px}

/* QUICK GRID */
.quick{display:grid;grid-template-columns:repeat(4,1fr);gap:8px}
@media(max-width:500px){.quick{grid-template-columns:repeat(2,1fr)}}
.qb{background:var(--bg1);border-radius:var(--r);padding:.7rem .5rem;text-align:center;cursor:pointer;border:none;font-size:11px;font-weight:500;color:var(--t2)}
.qb:hover{background:var(--bluelight);color:var(--blue)}
.qb-icon{font-size:22px;color:var(--blue);margin-bottom:4px}

/* PROTOTYPE BANNER */
.proto-banner{background:#FFF7E0;border-bottom:1px solid #E8D48A;padding:8px 18px;font-size:11px;color:#7a6010;display:flex;align-items:center;gap:6px}
</style>
</head>
<body>

<div class="proto-banner">⚠️ This is a visual prototype — no real backend or data. Interactions are simulated. See the attached Feature Spec document for full behavior rules.</div>

<!-- TOP NAV — management only (hidden in employee/login views) -->
<nav class="topnav" id="mgmt-nav" style="display:none">
  <div class="nav-logo">🏥 Ulluriaq Scheduling</div>
  <div class="nav-item" onclick="page('schedules',this)">Schedules</div>
  <div class="nav-item" onclick="page('overview',this)">Overview</div>
  <div class="nav-item" onclick="page('switchmgmt',this)">Switch requests <span class="nav-badge">2</span></div>
  <div class="nav-item" onclick="page('dropshiftmgmt',this)">Drop requests <span class="nav-badge">2</span></div>
  <div class="nav-item" onclick="page('unfilledmgmt',this)">Unfilled shifts <span class="nav-badge" style="background:#c0392b">7</span></div>
  <div class="nav-item" onclick="page('negtimes',this)">Partial shifts <span class="nav-badge">2</span></div>
  <div class="nav-item" onclick="page('bookoffs',this)">Book-offs <span class="nav-badge">4</span></div>
  <div class="nav-item" onclick="page('ot',this)">Overtime</div>
  <div class="nav-item" onclick="page('availability',this)">Availability</div>
  <div class="nav-item" onclick="page('oncall',this)">On-call <span class="nav-badge">1</span></div>
  <div class="nav-item" onclick="page('roster',this)">Shift roster</div>
  <div class="nav-item" onclick="page('empprofile',this)">Staff profiles</div>
  <div class="nav-item" onclick="page('loanservice',this)">Loan of service</div>
  <div class="nav-item" onclick="page('regularcontact',this)">Regular contact</div>
  <div class="nav-item" onclick="page('messaging',this)">Messaging</div>
  <div class="nav-item" onclick="page('memos',this)">Memos</div>
  <div class="nav-item" onclick="page('deadlines',this)">Deadlines</div>
  <div class="nav-item" onclick="page('weeklysummary',this)">Weekly summary</div>
  <div class="nav-item" onclick="page('leave',this)">Staff on leave 🔒</div>
  <div class="nav-item" onclick="page('staff',this)">Staff & access</div>
  <div class="nav-item" onclick="page('seniority',this)">Seniority</div>
  <div class="nav-item" onclick="page('codes',this)">Codes</div>
  <div class="nav-right">
    <span class="role-label">Logged in as: Management</span>
    <button class="role-switch" onclick="logout()">Sign out</button>
  </div>
</nav>

<!-- TOP NAV — employee -->
<nav class="topnav" id="emp-nav" style="display:none">
  <div class="nav-logo">🏥 Ulluriaq Scheduling</div>
  <div class="nav-item" onclick="empPage('emp-schedule',this)">My schedule</div>
  <div class="nav-item" onclick="empPage('emp-notifications',this)">Notifications <span class="nav-badge">3</span></div>
  <div class="nav-item" onclick="empPage('emp-switchshift',this)">Shift switch <span class="nav-badge">1</span></div>
  <div class="nav-item" onclick="empPage('emp-dropshift',this)">Drop a shift</div>
  <div class="nav-item" onclick="empPage('emp-unfilled',this)">Unfilled shifts</div>
  <div class="nav-item" onclick="empPage('emp-negtimes',this)">Partial shifts</div>
  <div class="nav-item" onclick="empPage('emp-bookoff',this)">Book-off request</div>
  <div class="nav-item" onclick="empPage('emp-messaging',this)">Messages</div>
  <div class="nav-item" onclick="empPage('emp-oncall',this)">On-call info</div>
  <div class="nav-item" onclick="empPage('emp-availability',this)">Availability</div>
  <div class="nav-item" onclick="empPage('emp-ot-avail',this)">OT availability</div>
  <div class="nav-item" onclick="empPage('emp-switches',this)">Switch history</div>
  <div class="nav-item" onclick="empPage('emp-seniority',this)">Seniority list</div>
  <div class="nav-item" onclick="empPage('emp-stats',this)">My shifts</div>
  <div class="nav-item" onclick="empPage('emp-codes',this)">Codes</div>
  <div class="nav-right">
    <span class="role-label">Keith Burnett · Boys IA</span>
    <button class="role-switch" onclick="logout()">Sign out</button>
  </div>
</nav>

<div class="main">

<!-- ==================== LOGIN ==================== -->
<div id="p-login" class="page on">
  <div class="login-wrap">
    <div class="login-card">
      <div class="login-logo"><div class="login-mark">📅</div><div><div class="login-title">Ulluriaq Scheduling</div><div class="login-sub">Ungava Tulattavik Health Center</div></div></div>
      <div class="role-seg">
        <div class="role-opt on" onclick="setRole('mgmt',this)">Management</div>
        <div class="role-opt" onclick="setRole('emp',this)">Employee</div>
      </div>
      <div class="field"><label>Work email</label><input type="email" placeholder="firstname.lastname.cstu@ssss.gouv.qc.ca"></div>
      <div class="field"><label>Password</label><input type="password" placeholder="••••••••"></div>
      <button class="btn pri" style="width:100%;padding:10px 0;margin-top:4px" id="sign-btn" onclick="doLogin()">Sign in</button>
      <div class="otp-note">🔐 Email + OTP verification is required only on first sign-in, and once every 12 months — not every login.</div>
      <div class="login-link"><a onclick="alert('Password reset instructions sent to your work email.')">Forgot password?</a></div>
    </div>
  </div>
</div>

<!-- ==================== MANAGEMENT: OVERVIEW ==================== -->
<div id="p-overview" class="page">
  <div class="grid4">
    <div class="stat"><div class="stat-n">43</div><div class="stat-l">Active staff</div></div>
    <div class="stat"><div class="stat-n" style="color:var(--red)">4</div><div class="stat-l">Pending book-offs</div></div>
    <div class="stat"><div class="stat-n" style="color:var(--blue)">7</div><div class="stat-l">Unfilled shifts</div></div>
    <div class="stat"><div class="stat-n" style="color:var(--green)">12</div><div class="stat-l">OT this PP</div></div>
  </div>
  <div class="grid2">
    <div class="card">
      <div class="card-title">Recent activity</div>
      <div style="font-size:12px">
        <div style="display:flex;justify-content:space-between;padding:6px 0;border-bottom:1px solid var(--bd)"><span>Eddy Bathalien's book-off (Jun 14, 19) approved</span><span style="color:var(--t3);font-size:10px">2h ago</span></div>
        <div style="display:flex;justify-content:space-between;padding:6px 0;border-bottom:1px solid var(--bd)"><span>Switch: Kerwin ↔ Mahkeda — approved</span><span style="color:var(--t3);font-size:10px">4h ago</span></div>
        <div style="display:flex;justify-content:space-between;padding:6px 0;border-bottom:1px solid var(--bd)"><span>OT offered to Gilles Lezi — Sat Jun 20, pending</span><span style="color:var(--t3);font-size:10px">6h ago</span></div>
        <div style="display:flex;justify-content:space-between;padding:6px 0"><span>Jalen Matandi's availability sheet — late</span><span style="color:var(--t3);font-size:10px">Yesterday</span></div>
      </div>
    </div>
    <div class="card">
      <div class="card-title">Shift coverage — by department</div>
      <div class="dep-row"><span>Boys Educators</span><div class="bar-bg"><div class="bar-fill" style="width:92%"></div></div><span>92%</span></div>
      <div class="dep-row"><span>Boys IA</span><div class="bar-bg"><div class="bar-fill" style="width:88%"></div></div><span>88%</span></div>
      <div class="dep-row"><span>Girls Educators</span><div class="bar-bg"><div class="bar-fill" style="width:79%;background:var(--pink)"></div></div><span>79%</span></div>
      <div class="dep-row"><span>Girls IA</span><div class="bar-bg"><div class="bar-fill" style="width:84%;background:var(--pink)"></div></div><span>84%</span></div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">Quick actions</div>
    <div class="quick">
      <button class="qb" onclick="page('schedules',null)"><div class="qb-icon">📅</div>Schedules</button>
      <button class="qb" onclick="page('ot',null)"><div class="qb-icon">⏰</div>Overtime</button>
      <button class="qb" onclick="page('bookoffs',null)"><div class="qb-icon">📋</div>Book-offs</button>
      <button class="qb" onclick="page('messaging',null)"><div class="qb-icon">💬</div>Messaging</button>
      <button class="qb" onclick="page('memos',null)"><div class="qb-icon">📝</div>Memos</button>
      <button class="qb" onclick="page('leave',null)"><div class="qb-icon">🛌</div>Staff leave</button>
      <button class="qb" onclick="page('staff',null)"><div class="qb-icon">👥</div>Staff access</button>
      <button class="qb" onclick="page('seniority',null)"><div class="qb-icon">📊</div>Seniority</button>
    </div>
  </div>
</div>

<!-- ==================== SCHEDULES ==================== -->
<div id="p-schedules" class="page">
  <div style="display:flex;gap:6px;margin-bottom:.8rem;flex-wrap:wrap;align-items:center">
    <button class="btn" id="sched-tab-ia" onclick="schedTab('ia',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Intervention Agents</button>
    <button class="btn" id="sched-tab-ed" onclick="schedTab('ed',this)">Educators</button>
    <button class="btn sm" onclick="renameUnit('boys')" style="margin-left:auto">✏ Rename Boys unit</button>
    <button class="btn sm" onclick="renameUnit('girls')">✏ Rename Girls unit</button>
    <button class="btn sm" style="color:#c0392b;border-color:#f5c6cb" onclick="removeSchedule()">🗑 Remove a schedule</button>
  </div>

  <!-- IA SCHEDULES -->
  <div id="sched-panel-ia">
    <div class="info">Intervention Agents schedule — click any row to open the full editable 4-week grid. Management can click any cell in the grid to edit times, add a coverage name, or apply a leave/book-off code. Transport and escort shifts appear as their own rows at the bottom of each pay-period week.</div>
    <div class="card">
      <div class="card-title">IA Schedules — PP 07 & 08</div>
      <table class="bt"><thead><tr><th>Unit</th><th>Coverage</th><th>Shifts</th><th></th></tr></thead><tbody>
        <tr><td><b>Boys IA</b></td><td>88%</td><td>J1/J2/S1/S2/N/OT/TRAN/ESC</td><td><button class="btn sm pri" onclick="showFullGrid('Boys IA',schedStaffIA)">Open grid</button></td></tr>
        <tr><td><b>Girls IA</b></td><td>84%</td><td>J1/J2/S1/S2/N/OT/TRAN/ESC</td><td><button class="btn sm pri" onclick="showFullGrid('Girls IA',schedStaffIA)">Open grid</button></td></tr>
      </tbody></table>
    </div>
  </div>

  <!-- EDUCATOR SCHEDULES -->
  <div id="sched-panel-ed" style="display:none">
    <div class="info">Educators schedule — separate list from IAs. Click any row to open the full editable 4-week grid.</div>
    <div class="card">
      <div class="card-title">Educator Schedules — PP 07 & 08</div>
      <table class="bt"><thead><tr><th>Unit</th><th>Coverage</th><th>Shifts</th><th></th></tr></thead><tbody>
        <tr><td><b>Boys Educators</b></td><td>92%</td><td>J1/J2/S1/S2/N/OT</td><td><button class="btn sm pri" onclick="showFullGrid('Boys Educators',schedStaffEd)">Open grid</button></td></tr>
        <tr><td><b>Girls Educators</b></td><td>79%</td><td>J1/J2/S1/S2/N/OT</td><td><button class="btn sm pri" onclick="showFullGrid('Girls Educators',schedStaffEd)">Open grid</button></td></tr>
      </tbody></table>
    </div>
  </div>

  <div id="full-grid-area"></div>
</div>

<!-- ==================== OVERTIME ==================== -->
<div id="p-ot" class="page">
  <div class="info">Open shift: Boys Educators — Sat Jun 20, S1 (15:00–22:45). Offer order: FT by seniority → PT by rotation → Recall → Agency. <b>Management-only view.</b> Employees never see who else was contacted, refused, or didn't answer.</div>
  <div class="card">
    <div class="card-title">Step 1 — Full-time educators, by seniority <span style="font-size:11px;color:var(--t3);font-weight:400">OT counts: equal distribution required — no junior FT can exceed a senior FT</span></div>
    <table class="bt"><thead><tr><th>#</th><th>Name</th><th>Status</th><th>OT this PP</th><th>Contacted</th><th>Result</th><th>Action</th></tr></thead><tbody>
      <tr style="opacity:.55"><td>1</td><td><b>Gilles Lezi</b></td><td><span class="badge b-ft">FT</span></td><td>2</td><td><span style="color:var(--t3)">Jun 18, 10:14 AM</span></td><td><span class="badge b-ter">R — Refused</span></td><td><span style="font-size:10px;color:var(--t3)">Moved on → Eddy Bathalien</span></td></tr>
      <tr style="background:#FFFCE8"><td>2</td><td><b>Eddy Bathalien</b></td><td><span class="badge b-ft">FT</span></td><td>1</td><td><input type="text" id="ot-contact-time" placeholder="e.g. Jun 18, 11:05 AM" style="font-size:10px;padding:3px 6px;border-radius:4px;border:1px solid var(--bd2);width:130px"></td><td><span style="font-size:10px;color:var(--amber);font-weight:600">⏳ Awaiting response</span></td><td><button class="btn sm grn" onclick="otAction('Eddy Bathalien','T')">T — Taken</button> <button class="btn sm red" onclick="otAction('Eddy Bathalien','R')">R — Refused</button> <button class="btn sm" onclick="otAction('Eddy Bathalien','NA')">No answer</button></td></tr>
      <tr style="opacity:.4"><td>3</td><td><b>Makeda Samuels</b></td><td><span class="badge b-ft">FT</span></td><td>2</td><td>—</td><td>—</td><td><span style="font-size:10px;color:var(--t3)">Next in queue</span></td></tr>
      <tr style="opacity:.4"><td>4</td><td><b>Michael Flemming</b></td><td><span class="badge b-ft">FT</span></td><td>1</td><td>—</td><td>—</td><td><span style="font-size:10px;color:var(--t3)">Next in queue</span></td></tr>
    </tbody></table>
  </div>
  <div id="ot-result"></div>
</div>

<!-- ==================== BOOK-OFFS ==================== -->
<div id="p-bookoffs" class="page">
  <div class="info">Requests under 24 hrs are auto-denied before reaching this queue. 3+ consecutive days = vacation approval required. 3 consecutive weekend book-offs triggers an automatic management alert.</div>
  <div class="card">
    <div class="card-title">Pending book-off requests</div>
    <table class="bt" id="bo-mgmt-table"></table>
  </div>
</div>

<!-- ==================== MESSAGING ==================== -->
<div id="p-messaging" class="page">
  <p style="font-size:12px;color:var(--t2);margin-bottom:.8rem">Direct messaging between employees. Use "Propose switch" inside a conversation to start the formal 3-step switch approval chain.</p>
  <div id="msg-area"></div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Switch approval queue (management)</div>
    <div class="info">Only requests where BOTH employees have already agreed appear here. Three-way switches are never permitted.</div>
    <table class="bt"><thead><tr><th>Employees</th><th>Details</th><th>Both agreed</th><th>Action</th></tr></thead><tbody>
      <tr><td><b>Wesley Thomas ↔ Jema Rattray</b></td><td>Jun 23 (S/T) ↔ Jun 24 (J1) · Girls Educators</td><td style="color:var(--green)">✓ 9:22 AM</td><td><button class="btn sm grn" onclick="notify('Switch approved. Both employees notified by app + email. Schedule updated.')">Approve</button> <button class="btn sm red" onclick="notify('Switch denied. Both employees notified.')">Deny</button></td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== MEMOS ==================== -->
<div id="p-memos" class="page">
  <div style="display:flex;gap:6px;margin-bottom:.9rem;border-bottom:1px solid var(--bd);padding-bottom:.6rem">
    <button class="btn" id="memo-tab-tran" onclick="memoTab('tran',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Transport & Escort</button>
    <button class="btn" id="memo-tab-gen" onclick="memoTab('gen',this)">General memos</button>
    <button class="btn" id="memo-tab-dm" onclick="memoTab('dm',this)">Direct message</button>
  </div>

  <!-- Transport & Escort -->
  <div id="memo-panel-tran">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.8rem">
      <div style="font-size:12px;color:var(--t2)">Transportation and northern escort details — linked to TRAN/ESC cells on the schedule grid.</div>
      <button class="btn pri" onclick="openModal('new-memo-modal')">+ New memo</button>
    </div>
    <div id="memo-list"></div>
  </div>

  <!-- General memos -->
  <div id="memo-panel-gen" style="display:none">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.8rem">
      <div style="font-size:12px;color:var(--t2)">Broadcast memos sent to all staff, a specific unit, or a specific role. All memos are logged below.</div>
      <button class="btn pri" onclick="openModal('new-genmemo-modal')">+ New general memo</button>
    </div>
    <div id="genmemo-list"></div>
  </div>

  <!-- Direct message from management -->
  <div id="memo-panel-dm" style="display:none">
    <div class="info">Send a direct message to one employee from management. The employee receives an in-app notification and email.</div>
    <div class="card" style="max-width:500px">
      <div class="card-title">New direct message</div>
      <div class="field"><label>To (employee)</label>
        <select id="dm-to">
          <option>Keith Burnett</option><option>Gilles Lezi</option><option>Eddy Bathalien</option><option>Makeda Samuels</option><option>Jean Nicolas Michaud</option><option>Mark D'Agostino</option><option>Greg Page</option><option>Angelo Kontakos</option><option>Kerwin Guy-Roach</option><option>Shannon Ridley</option>
        </select>
      </div>
      <div class="field"><label>From</label>
        <select id="dm-from"><option>Scheduling Admin</option><option>Unit Manager</option><option>On-call Manager</option></select>
      </div>
      <div class="field"><label>Subject</label><input type="text" id="dm-subject" placeholder="e.g. Schedule change — Jun 20"></div>
      <div class="field"><label>Message</label><textarea id="dm-body" rows="4" placeholder="Type your message..."></textarea></div>
      <button class="btn pri" style="width:100%" onclick="sendDM()">Send message</button>
    </div>
    <div class="card" style="margin-top:.8rem">
      <div class="card-title">Sent messages log</div>
      <table class="bt" id="dm-log-table"></table>
    </div>
  </div>
</div>

<!-- ==================== STAFF ON LEAVE ==================== -->
<div id="p-leave" class="page">
  <div class="info">🔒 Never visible to employees in general. Exception: an employee on leave sees their own progressive return schedule in their personal view only.</div>
  <div class="card">
    <div class="card-title">Staff on leave tracker <button class="btn sm pri" onclick="openModal('new-leave-modal')">+ Add record</button></div>
    <table class="bt"><thead><tr><th>Name</th><th>Type</th><th>Started</th><th>Return</th><th>Progressive return</th><th></th></tr></thead><tbody>
      <tr><td>Sergio De Luca</td><td><span class="badge b-vac">Vacation</span></td><td>Jun 15</td><td>Jun 20</td><td>No</td><td><button class="btn sm">Edit</button></td></tr>
      <tr><td>Ashley Zycholtz</td><td><span class="badge b-sick">Sick leave</span></td><td>Jun 10</td><td>Jul 15</td><td>Yes — 2 shifts/wk for 2 wks, then full schedule</td><td><button class="btn sm">Edit</button></td></tr>
      <tr><td>Darius Branch</td><td><span class="badge b-cnesst">CNESST leave</span></td><td>May 20</td><td>Aug 1</td><td>Yes — 3 shifts/wk for 4 wks, reassessed by physician</td><td><button class="btn sm">Edit</button></td></tr>
      <tr><td>Stephanie George</td><td><span class="badge b-mat">Maternity leave</span></td><td>Mar 1</td><td>Feb 28, 2027</td><td>No</td><td><button class="btn sm">Edit</button></td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== STAFF ACCESS ==================== -->
<div id="p-staff" class="page">
  <div class="info">Suspending or terminating immediately revokes app login access. Reinstating restores it instantly. Historical schedule data is retained regardless of status.</div>
  <div class="card">
    <div class="card-title">Staff & access control</div>
    <div style="display:flex;gap:8px;margin-bottom:.8rem"><input type="text" placeholder="Search by name, unit, or role..." style="padding:7px 10px;border-radius:var(--r);border:1px solid var(--bd2);font-size:12px;flex:1"></div>
    <table class="bt"><thead><tr><th>Name</th><th>Role · Unit</th><th>Status</th><th>App access</th><th>Action</th></tr></thead><tbody>
      <tr><td><b>Gilles Lezi</b></td><td>Educator FT · Boys</td><td><span class="badge b-act">Active</span></td><td>✓ Can sign in</td><td><button class="btn sm amb">Suspend</button> <button class="btn sm red">Terminate</button></td></tr>
      <tr><td><b>Eddy Bathalien</b></td><td>Educator FT · Boys</td><td><span class="badge b-act">Active</span></td><td>✓ Can sign in</td><td><button class="btn sm amb">Suspend</button> <button class="btn sm red">Terminate</button></td></tr>
      <tr style="background:#FFFBF0"><td><b>Wesley Thomas</b><div style="font-size:10px;color:var(--t3)">Pending HR review · since Jun 10</div></td><td>Educator TFT · Girls</td><td><span class="badge b-sus">Suspended</span></td><td>✗ Blocked</td><td><button class="btn sm grn" onclick="notify('Wesley Thomas reinstated. Access restored immediately.')">Reinstate</button> <button class="btn sm red">Terminate</button></td></tr>
      <tr style="background:#FEF5F5;opacity:.75"><td><b>Jalen Matandi</b><div style="font-size:10px;color:var(--t3)">Resigned · since May 30</div></td><td>IA PT · Girls</td><td><span class="badge b-ter">Terminated</span></td><td>✗ Removed</td><td><button class="btn sm grn" onclick="notify('Jalen Matandi reinstated. Access restored.')">Reinstate</button></td></tr>
      <tr><td><b>Keith Burnett</b></td><td>IA FT · Boys</td><td><span class="badge b-act">Active</span></td><td>✓ Can sign in</td><td><button class="btn sm amb">Suspend</button> <button class="btn sm red">Terminate</button></td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== SENIORITY ==================== -->
<div id="p-seniority" class="page">
  <div class="info">Each job title has its own seniority list. Drag rows by ≡ or use ↑↓ to reorder. Order drives OT distribution and rotation. Add staff with their job title — they will appear only on the relevant list.</div>
  <div style="display:flex;gap:8px;margin-bottom:.9rem;flex-wrap:wrap;align-items:center">
    <button id="sen-tab-ed" class="btn" onclick="senTab('educators',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Educators</button>
    <button id="sen-tab-ia" class="btn" onclick="senTab('ia',this)">Intervention Agents</button>
    <button class="btn pri" style="margin-left:auto" onclick="openModal('add-sen-modal')">+ Add staff member</button>
  </div>
  <div id="sen-title-row" style="display:flex;align-items:center;gap:10px;margin-bottom:.5rem">
    <span id="sen-unit-label" style="font-weight:600;font-size:13px"></span>
    <button class="btn sm" onclick="renameSenUnit()" style="font-size:10px">✏ Rename unit</button>
  </div>
  <ul class="sen-list" id="sen-list"></ul>
  <button class="btn pri" style="margin-top:.5rem" onclick="notify('Seniority order saved. This now drives OT distribution and rotation.')">Save order</button>
</div>

<!-- ==================== EMPLOYEE: SCHEDULE ==================== -->
<div id="p-emp-schedule" class="page">
  <div class="sched-tabs" id="emp-sched-tabs">
    <div class="st on" onclick="empSchedTab('boys-ia',this)">Boys IA <span class="pin hp" title="Home screen — pinned">📌</span></div>
    <div class="st" onclick="empSchedTab('boys-ed',this)">Boys Educators <span class="pin" onclick="event.stopPropagation();setEmpHome(this)">📍</span></div>
    <div class="st" onclick="empSchedTab('girls-ia',this)">Girls IA <span class="pin" onclick="event.stopPropagation();setEmpHome(this)">📍</span></div>
    <div class="st" onclick="empSchedTab('girls-ed',this)">Girls Educators <span class="pin" onclick="event.stopPropagation();setEmpHome(this)">📍</span></div>
  </div>
  <div id="sp-boys-ia" class="sched-panel on" style="overflow-x:auto"></div>
  <div id="sp-boys-ed" class="sched-panel"><div class="home-banner">📍 Boys Educators — click 📍 above to make this your home screen.</div><p style="font-size:12px;color:var(--t2)">Full Boys Educators 4-week grid loads here.</p></div>
  <div id="sp-girls-ia" class="sched-panel"><div class="home-banner">📍 Girls IA — click 📍 above to make this your home screen.</div><p style="font-size:12px;color:var(--t2)">Full Girls IA 4-week grid loads here.</p></div>
  <div id="sp-girls-ed" class="sched-panel"><div class="home-banner">📍 Girls Educators — click 📍 above to make this your home screen.</div><p style="font-size:12px;color:var(--t2)">Full Girls Educators 4-week grid loads here.</p></div>
</div>

<!-- ==================== EMPLOYEE: BOOK-OFF ==================== -->
<div id="p-emp-bookoff" class="page">
  <div class="info">Leave type is required before you can submit. Requests under 24 hrs are automatically denied — contact management directly instead.</div>
  <div class="card" style="max-width:460px">
    <div class="card-title">Request a book-off</div>
    <div class="field"><label>Date(s) requesting off</label><input type="date" id="bo-date" onchange="check24(this.value)"></div>
    <div id="u24-warn" style="display:none;background:var(--redlight);color:var(--red);border-radius:var(--r);padding:9px 12px;font-size:12px;margin-bottom:.8rem">🚫 Less than 24 hours away — this request cannot be submitted. Contact management directly.</div>
    <div class="field"><label>Leave type <span style="color:var(--red)">* required</span></label>
      <div class="ltabs">
        <div class="ltab" onclick="selLeave(this,'Vacation')">Vacation</div>
        <div class="ltab" onclick="selLeave(this,'Sick')">Sick</div>
        <div class="ltab" onclick="selLeave(this,'Stat')">Stat</div>
        <div class="ltab" onclick="selLeave(this,'Psychosocial')">Psychosocial</div>
        <div class="ltab" onclick="selLeave(this,'LIB')">LIB</div>
        <div class="ltab" onclick="selLeave(this,'Mat leave')">Mat leave</div>
      </div>
    </div>
    <div id="leave-err" style="display:none;color:var(--red);font-size:11px;margin-bottom:.5rem">⚠️ Select a leave type to continue.</div>
    <div class="field"><label>Notes (optional)</label><input type="text" placeholder="Any additional details..."></div>
    <button class="btn pri" style="width:100%" onclick="submitBO()">Submit request</button>
  </div>
</div>

<!-- ==================== EMPLOYEE: UNFILLED SHIFTS / NEGOTIATED TIMES ==================== -->
<div id="p-emp-unfilled" class="page">
  <div class="info">Shifts highlighted in yellow below could not be filled through regular OT rotation. If you can help cover part of the shift, enter the times you're able to work and submit for management approval.</div>
  <div class="card">
    <div class="card-title">Open unfilled shifts — your unit</div>
    <table class="bt" id="unfilled-table"></table>
  </div>
</div>

<!-- ==================== MGMT: NEGOTIATED TIME APPROVALS ==================== -->
<div id="p-negtimes" class="page">
  <div class="info">Employees have submitted partial availability for unfilled shifts. Review and approve or deny each request. Approved times are added to the schedule with the employee's name and adjusted hours noted.</div>
  <div class="card">
    <div class="card-title">Negotiated time requests — pending approval</div>
    <table class="bt" id="negtime-mgmt-table"></table>
  </div>
</div>

<!-- ==================== MANAGEMENT: SWITCH REQUESTS ==================== -->
<div id="p-switchmgmt" class="page">
  <div class="info">Review shift switch requests submitted by staff. Both employees must agree, then management approves. Once approved, the switch is held until the scheduler pushes it live.</div>
  <div class="card">
    <div class="card-title">Pending switch requests</div>
    <table class="bt"><thead><tr><th>Requested</th><th>From</th><th>Gives up</th><th>Receives</th><th>With</th><th>Status</th><th>Action</th></tr></thead><tbody>
      <tr>
        <td>Oct 16, 2026</td>
        <td>Keith Burnett</td>
        <td>Wed Oct 22 — J1 Day</td>
        <td>Tue Oct 21 — S1 Evening</td>
        <td>Angelo Kontakos</td>
        <td><span class="badge" style="background:#FFF8E1;color:#B8860B">Awaiting peer confirm</span></td>
        <td><button class="btn sm" onclick="notify('Switch approved — schedule updated at next push.')">Approve</button> <button class="btn sm" style="background:#FFF3F3;color:var(--red)" onclick="notify('Switch denied. Both employees notified.')">Deny</button></td>
      </tr>
      <tr>
        <td>Oct 14, 2026</td>
        <td>Greg Page</td>
        <td>Sat Oct 25 — S1 Evening</td>
        <td>Sun Oct 26 — J1 Day</td>
        <td>Jean-N. Michaud</td>
        <td><span class="badge" style="background:#E8F5E9;color:#2e7d32">Both agreed</span></td>
        <td><button class="btn sm pri" onclick="notify('Switch approved — schedule updated at next push.')">Approve</button> <button class="btn sm" style="background:#FFF3F3;color:var(--red)" onclick="notify('Switch denied. Both employees notified.')">Deny</button></td>
      </tr>
    </tbody></table>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Approved switches — pending push</div>
    <div class="info">These switches are approved but not yet visible to employees. They go live at the next Mon/Wed/Fri scheduler push.</div>
    <table class="bt"><thead><tr><th>Approved</th><th>Employee 1</th><th>Gave up</th><th>Employee 2</th><th>Gave up</th></tr></thead><tbody>
      <tr>
        <td>Oct 12, 2026</td><td>Steven Yearwood</td><td>Mon Oct 20 — S1</td><td>Keon Pompey</td><td>Mon Oct 20 — J1</td>
      </tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== MANAGEMENT: UNFILLED SHIFTS ==================== -->
<div id="p-unfilledmgmt" class="page">
  <div class="info">All currently unfilled shifts. Contact staff via OT rotation or recall process. Mark shifts as filled once covered.</div>
  <div class="card">
    <div class="card-title">Unfilled shifts — action required</div>
    <table class="bt"><thead><tr><th>Date</th><th>Unit</th><th>Shift</th><th>Reason</th><th>Priority</th><th>Action</th></tr></thead><tbody>
      <tr style="background:#FFF8F8">
        <td><b>Mon Oct 20</b></td><td>Boys IA</td><td>J1 — 07:00–14:45</td><td>Book-off (Keon Pompey — SICK)</td><td><span class="badge b-red">Urgent</span></td>
        <td><button class="btn sm pri" onclick="notify('OT rotation started for Boys IA J1 Oct 20.')">Start OT rotation</button></td>
      </tr>
      <tr>
        <td><b>Wed Oct 22</b></td><td>Girls Educators</td><td>S1 — 15:00–22:45</td><td>CNR — understaffed</td><td><span class="badge b-sus">Medium</span></td>
        <td><button class="btn sm" onclick="notify('Recall call started for Girls Educators S1 Oct 22.')">Recall call</button></td>
      </tr>
      <tr>
        <td><b>Fri Oct 24</b></td><td>Boys IA</td><td>N — 22:30–07:00</td><td>No night coverage</td><td><span class="badge" style="background:var(--bg1);color:var(--t2)">Low</span></td>
        <td><button class="btn sm" onclick="notify('Posting to recall list.')">Post recall</button></td>
      </tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== CODES REFERENCE ==================== -->
<div id="p-codes" class="page">
  <div class="card">
    <div class="card-title">Schedule & leave codes — reference guide</div>
    <div class="info" style="margin-bottom:1rem">These codes appear on the schedule and in requests. Management uses these when approving book-offs or placing leave on the schedule.</div>
    <table class="bt"><thead><tr><th>Code</th><th>Full name</th><th>Description</th></tr></thead><tbody>
      <tr><td><span class="badge" style="background:#FDECEA;color:#c0392b;font-size:12px;padding:3px 8px">VAC</span></td><td><b>Vacation</b></td><td>Approved paid vacation time.</td></tr>
      <tr><td><span class="badge" style="background:#E8EAF6;color:#3949AB;font-size:12px;padding:3px 8px">STAT</span></td><td><b>Statutory Holiday</b></td><td>Recognized public holiday — paid day off per collective agreement.</td></tr>
      <tr><td><span class="badge" style="background:#FFF3E0;color:#E65100;font-size:12px;padding:3px 8px">SICK</span></td><td><b>Sick</b></td><td>Unplanned sick leave. Medical note may be required for extended absences.</td></tr>
      <tr><td><span class="badge" style="background:#F3E5F5;color:#6A1B9A;font-size:12px;padding:3px 8px">PSYCH</span></td><td><b>Psychological Day</b></td><td>Mental health day per collective agreement. Limited per year per employee.</td></tr>
      <tr><td><span class="badge" style="background:#E0F2F1;color:#00695C;font-size:12px;padding:3px 8px">TRAINING</span></td><td><b>Training</b></td><td>Scheduled training, workshop, or certification — paid leave.</td></tr>
      <tr><td><span class="badge" style="background:#E8F5E9;color:#2E7D32;font-size:12px;padding:3px 8px">PEXT</span></td><td><b>Bank Time</b></td><td>Banked overtime hours taken as time off instead of pay.</td></tr>
      <tr><td><span class="badge" style="background:#E3F2FD;color:#1565C0;font-size:12px;padding:3px 8px">OT-TAKEN</span></td><td><b>OT Taken</b></td><td>Overtime paid out or taken — used for tracking purposes on schedule.</td></tr>
      <tr><td><span class="badge" style="background:#FFF8E1;color:#F57F17;font-size:12px;padding:3px 8px">AUTHO</span></td><td><b>Authorized Without Pay</b></td><td>Approved absence — unpaid per agreement. Must be pre-authorized by management.</td></tr>
      <tr><td><span class="badge" style="background:#ADD8E6;color:#0C447C;font-size:12px;padding:3px 8px">OT</span></td><td><b>Overtime</b></td><td>Overtime shift — above regular scheduled hours.</td></tr>
      <tr><td><span class="badge" style="background:#D7E8FF;color:#1a3a6e;font-size:12px;padding:3px 8px">SW</span></td><td><b>Shift Switch</b></td><td>Shift was swapped with another employee — both names shown on the schedule.</td></tr>
      <tr><td><span class="badge" style="background:#FFF9C4;color:#6D4C41;font-size:12px;padding:3px 8px">TRAN</span></td><td><b>Transport</b></td><td>Youth transportation assignment — shown in dedicated TRAN row on IA schedules.</td></tr>
      <tr><td><span class="badge" style="background:#FFE0B2;color:#BF360C;font-size:12px;padding:3px 8px">ESC</span></td><td><b>Escort</b></td><td>Youth escort (travel/overnight) — shown in dedicated ESC row on IA schedules.</td></tr>
      <tr><td><span class="badge" style="background:var(--bg2);color:var(--t2);font-size:12px;padding:3px 8px">R</span></td><td><b>Rest Day</b></td><td>Scheduled rest day — not a work day.</td></tr>
    </tbody></table>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Shift codes</div>
    <table class="bt"><thead><tr><th>Code</th><th>Shift</th><th>Typical hours</th></tr></thead><tbody>
      <tr><td><b>J1</b></td><td>Day shift 1</td><td>07:00 – 14:45</td></tr>
      <tr><td><b>J2</b></td><td>Day shift 2</td><td>07:30 – 15:15</td></tr>
      <tr><td><b>J/S</b></td><td>Day-to-Evening overlap</td><td>09:00 – 17:00</td></tr>
      <tr><td><b>S1</b></td><td>Evening shift 1</td><td>15:00 – 22:45</td></tr>
      <tr><td><b>S2</b></td><td>Evening shift 2</td><td>15:30 – 23:15</td></tr>
      <tr><td><b>N</b></td><td>Night shift</td><td>22:30 – 07:00</td></tr>
      <tr><td><b>J1/T</b></td><td>Day shift (training day)</td><td>07:00 – 14:45 + training hours</td></tr>
      <tr><td><b>S1/T</b></td><td>Evening shift (training day)</td><td>15:00 – 22:45 + training hours</td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: CODES (read-only view) ==================== -->
<div id="p-emp-codes" class="page">
  <div class="card">
    <div class="card-title">Schedule &amp; leave codes — reference guide</div>
    <div class="info" style="margin-bottom:1rem">These codes appear on your schedule. You can view what each code means here. Only management or a scheduler can apply or change codes on the schedule.</div>
    <table class="bt"><thead><tr><th>Code</th><th>Full name</th><th>What it means for you</th></tr></thead><tbody>
      <tr><td><span class="badge" style="background:#FDECEA;color:#c0392b;font-size:12px;padding:3px 8px">VAC</span></td><td><b>Vacation</b></td><td>Your approved vacation. Shows on your shift cell alongside the day's shift.</td></tr>
      <tr><td><span class="badge" style="background:#E8EAF6;color:#3949AB;font-size:12px;padding:3px 8px">STAT</span></td><td><b>Statutory Holiday</b></td><td>Public holiday — paid per collective agreement.</td></tr>
      <tr><td><span class="badge" style="background:#FFF3E0;color:#E65100;font-size:12px;padding:3px 8px">SICK</span></td><td><b>Sick</b></td><td>Sick day entered by management once you call in.</td></tr>
      <tr><td><span class="badge" style="background:#F3E5F5;color:#6A1B9A;font-size:12px;padding:3px 8px">PSYCH</span></td><td><b>Psychological Day</b></td><td>Mental health day per collective agreement.</td></tr>
      <tr><td><span class="badge" style="background:#E0F2F1;color:#00695C;font-size:12px;padding:3px 8px">TRAINING</span></td><td><b>Training</b></td><td>You're scheduled for training on this shift.</td></tr>
      <tr><td><span class="badge" style="background:#E8F5E9;color:#2E7D32;font-size:12px;padding:3px 8px">PEXT</span></td><td><b>Bank Time</b></td><td>Banked OT hours being taken as time off.</td></tr>
      <tr><td><span class="badge" style="background:#E3F2FD;color:#1565C0;font-size:12px;padding:3px 8px">OT-TAKEN</span></td><td><b>OT Taken</b></td><td>Overtime tracked — paid out or banked.</td></tr>
      <tr><td><span class="badge" style="background:#FFF8E1;color:#F57F17;font-size:12px;padding:3px 8px">AUTHO</span></td><td><b>Authorized Without Pay</b></td><td>Pre-approved unpaid absence.</td></tr>
      <tr><td><span class="badge" style="background:#D7E8FF;color:#1a3a6e;font-size:12px;padding:3px 8px">SW</span></td><td><b>Shift Switch</b></td><td>You switched this shift — partner name shows on the cell.</td></tr>
      <tr><td><span class="badge" style="background:#FFF9C4;color:#6D4C41;font-size:12px;padding:3px 8px">TRAN</span></td><td><b>Transport</b></td><td>Transport assignment — shown in the TRAN row at the bottom of the schedule.</td></tr>
      <tr><td><span class="badge" style="background:#FFE0B2;color:#BF360C;font-size:12px;padding:3px 8px">ESC</span></td><td><b>Escort</b></td><td>Youth escort assignment — see escort row on IA schedule.</td></tr>
      <tr><td><span class="badge" style="background:var(--bg2);color:var(--t2);font-size:12px;padding:3px 8px">R</span></td><td><b>Rest Day</b></td><td>Scheduled rest — not a work day.</td></tr>
    </tbody></table>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Shift codes</div>
    <table class="bt"><thead><tr><th>Code</th><th>Shift</th><th>Typical hours</th></tr></thead><tbody>
      <tr><td><b>J1</b></td><td>Day shift 1</td><td>07:00 – 14:45</td></tr>
      <tr><td><b>J2</b></td><td>Day shift 2</td><td>07:30 – 15:15</td></tr>
      <tr><td><b>J3</b></td><td>Day shift 3</td><td>08:00 – 16:00</td></tr>
      <tr><td><b>S1</b></td><td>Evening shift 1</td><td>15:00 – 22:45</td></tr>
      <tr><td><b>S2</b></td><td>Evening shift 2</td><td>15:30 – 23:15</td></tr>
      <tr><td><b>S3</b></td><td>Evening shift 3</td><td>16:00 – 00:00</td></tr>
      <tr><td><b>N</b></td><td>Night shift</td><td>22:30 – 07:00</td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: MY SHIFTS ==================== -->
<div id="p-emp-stats" class="page">
  <div class="info">Full-time staff are scheduled for <b>20 shifts total — 10 per pay period</b>. Each shift is accounted for: regular, overtime, leave, or a book-off with reason. Part-time staff see their individual block schedule below.</div>
  <!-- PP 07 summary -->
  <div class="card">
    <div class="card-title">Pay Period 07 — Jun 14–27, 2026 · 10 shifts</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:.8rem">
      <span class="badge b-ft" style="font-size:12px;padding:4px 10px">8 regular</span>
      <span class="badge" style="background:#ADD8E6;color:#0C447C;font-size:12px;padding:4px 10px">1 overtime</span>
      <span class="badge" style="background:#FDECEA;color:#c0392b;font-size:12px;padding:4px 10px">1 vacation</span>
    </div>
    <table class="bt"><thead><tr><th>Date</th><th>Shift</th><th>Type</th><th>Notes</th></tr></thead><tbody>
      <tr><td>Sat Jun 14</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Tue Jun 17</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Wed Jun 18</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Sat Jun 21</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Sun Jun 22</td><td>ESC — Escort</td><td><span class="badge" style="background:#ADD8E6;color:#0C447C">Overtime</span></td><td>Northern escort — Montreal court</td></tr>
      <tr style="background:#FFF8F8"><td>Mon Jun 23</td><td>J1 — 07:00–14:45</td><td><span class="badge" style="background:#FDECEA;color:#c0392b">Vacation (VAC)</span></td><td>Approved book-off — Jema R. covering</td></tr>
      <tr><td>Tue Jun 24</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Thu Jun 26</td><td>S1/T — 15:00–22:45</td><td><span class="badge b-ft">Regular (training)</span></td><td>Training attached to shift</td></tr>
      <tr><td>Fri Jun 27</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Sat Jun 28</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
    </tbody></table>
  </div>
  <!-- PP 08 summary -->
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Pay Period 08 — Jun 28–Jul 11, 2026 · 10 shifts</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:.8rem">
      <span class="badge b-ft" style="font-size:12px;padding:4px 10px">8 regular</span>
      <span class="badge" style="background:#ADD8E6;color:#0C447C;font-size:12px;padding:4px 10px">1 overtime</span>
      <span class="badge" style="background:#FFF3E0;color:#E65100;font-size:12px;padding:4px 10px">1 sick</span>
    </div>
    <table class="bt"><thead><tr><th>Date</th><th>Shift</th><th>Type</th><th>Notes</th></tr></thead><tbody>
      <tr><td>Sun Jun 29</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Mon Jun 30</td><td>J1 sw — 07:00–14:45</td><td><span class="badge b-ft">Regular (switch)</span></td><td>Switched with Angelo K. — approved</td></tr>
      <tr><td>Thu Jul 3</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr style="background:#FFF8F8"><td>Sat Jul 5</td><td>J1 — 07:00–14:45</td><td><span class="badge" style="background:#FFF3E0;color:#E65100">Sick (SICK)</span></td><td>Unplanned absence</td></tr>
      <tr><td>Sun Jul 6</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Mon Jul 7</td><td>OT — J1</td><td><span class="badge" style="background:#ADD8E6;color:#0C447C">Overtime</span></td><td>Coverage for Keon P. book-off</td></tr>
      <tr><td>Wed Jul 9</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Thu Jul 10</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Fri Jul 11</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
      <tr><td>Sat Jul 12</td><td>J1 — 07:00–14:45</td><td><span class="badge b-ft">Regular</span></td><td>—</td></tr>
    </tbody></table>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Year-to-date summary</div>
    <div class="grid4">
      <div class="stat"><div class="stat-n">20</div><div class="stat-l">Shifts this period (total)</div></div>
      <div class="stat"><div class="stat-n">16</div><div class="stat-l">Regular shifts</div></div>
      <div class="stat"><div class="stat-n" style="color:#0C447C">2</div><div class="stat-l">Overtime shifts</div></div>
      <div class="stat"><div class="stat-n" style="color:#c0392b">2</div><div class="stat-l">Book-offs (1 VAC · 1 SICK)</div></div>
    </div>
  </div>
</div>

<!-- ==================== EMPLOYEE: SENIORITY ==================== -->
<div id="p-emp-seniority" class="page">
  <div class="info">Read-only view. Seniority order determines overtime offers — most senior is offered first. Contact management for any corrections.</div>
  <div style="display:flex;gap:8px;margin-bottom:.8rem">
    <button class="btn" id="sen-emp-ed-btn" onclick="empSenUnit('educators',this)">Educators</button>
    <button class="btn" id="sen-emp-ia-btn" onclick="empSenUnit('ia',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Intervention Agents</button>
  </div>
  <div class="card">
    <div class="card-title" id="emp-sen-title">Intervention Agents — Seniority List</div>
    <table class="bt" id="emp-sen-table"></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: SWITCH HISTORY ==================== -->
<div id="p-emp-switches" class="page">
  <div class="info">All your approved shift switches. Management approval is required for every switch to take effect.</div>
  <div class="card">
    <div class="card-title">Approved switch history</div>
    <table class="bt"><thead><tr><th>Date approved</th><th>You gave up</th><th>You received</th><th>With</th><th>Unit</th></tr></thead><tbody>
      <tr>
        <td>Jun 12, 2026</td>
        <td>Tue Jun 23 — S/T Evening</td>
        <td>Wed Jun 24 — J1 Day</td>
        <td>Jema Rattray</td>
        <td>Girls Educators</td>
      </tr>
      <tr>
        <td>May 28, 2026</td>
        <td>Sat May 31 — J/S Day</td>
        <td>Fri May 30 — J1 Day</td>
        <td>Mahkeda Newton</td>
        <td>Boys IA</td>
      </tr>
      <tr>
        <td>Apr 14, 2026</td>
        <td>Sun Apr 20 — S1 Evening</td>
        <td>Sat Apr 19 — J1 Day</td>
        <td>Angelo Kontakos</td>
        <td>Boys IA</td>
      </tr>
      <tr>
        <td>Mar 3, 2026</td>
        <td>Fri Mar 7 — S1 Evening</td>
        <td>Mon Mar 10 — J1 Day</td>
        <td>Greg Page</td>
        <td>Boys IA</td>
      </tr>
    </tbody></table>
  </div>
  <div class="card">
    <div class="card-title">Pending switch requests</div>
    <table class="bt"><thead><tr><th>Status</th><th>You gave up</th><th>You receive</th><th>With</th><th>Stage</th></tr></thead><tbody>
      <tr>
        <td><span class="badge b-sus">Pending</span></td>
        <td>Fri Jul 11 — S/T Evening</td>
        <td>Thu Jul 10 — J1 Day</td>
        <td>Wesley Thomas</td>
        <td>⏳ Waiting for management approval</td>
      </tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: MESSAGING ==================== -->
<div id="p-emp-messaging" class="page">
  <div style="display:flex;gap:6px;margin-bottom:.8rem;flex-wrap:wrap">
    <button class="btn" id="emsg-tab-inbox" onclick="empMsgTab('inbox',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Inbox</button>
    <button class="btn" id="emsg-tab-compose" onclick="empMsgTab('compose',this)">New message</button>
    <button class="btn" id="emsg-tab-sent" onclick="empMsgTab('sent',this)">Sent</button>
  </div>
  <!-- INBOX -->
  <div id="emsg-panel-inbox">
    <div style="font-size:11px;color:var(--t3);margin-bottom:.5rem">Messages from management and colleagues. Use this for arrival times, shift questions, coverage requests, etc.</div>
    <div id="emp-inbox-list"></div>
  </div>
  <!-- COMPOSE -->
  <div id="emsg-panel-compose" style="display:none">
    <div class="card" style="max-width:500px">
      <div class="card-title">New message</div>
      <div class="field"><label>To</label>
        <select id="emp-msg-to" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
          <option value="">— Select recipient —</option>
          <optgroup label="Management">
            <option>Scheduling Admin</option><option>Unit Manager</option><option>On-call Manager</option>
          </optgroup>
          <optgroup label="Staff">
            <option>Gilles Lezi</option><option>Eddy Bathalien</option><option>Makeda Samuels</option><option>Jean Nicolas Michaud</option><option>Mark D'Agostino</option><option>Greg Page</option><option>Angelo Kontakos</option><option>Steven Yearwood</option><option>Keon Pompey</option><option>Shannon Ridley</option><option>Yvonne Kaberamanzi</option><option>Ansonia Arrington</option>
          </optgroup>
        </select>
      </div>
      <div class="field"><label>Subject / purpose</label>
        <select id="emp-msg-subject" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
          <option value="">— Select subject —</option>
          <option>Arriving late</option>
          <option>Requesting to come in earlier</option>
          <option>Requesting a shift switch</option>
          <option>Offering a shift</option>
          <option>Availability question</option>
          <option>General message</option>
        </select>
      </div>
      <div class="field"><label>Message</label><textarea id="emp-msg-body" rows="4" placeholder="Type your message..."></textarea></div>
      <button class="btn pri" style="width:100%" onclick="sendEmpMsg()">Send</button>
    </div>
  </div>
  <!-- SENT -->
  <div id="emsg-panel-sent" style="display:none">
    <div id="emp-sent-list"></div>
  </div>
</div>

<!-- ==================== EMPLOYEE: SHIFT SWITCH ==================== -->
<div id="p-emp-switchshift" class="page">
  <div class="info">Request to swap a shift with a colleague. Both employees must agree before it goes to management for approval. Three-way switches are not permitted.</div>
  <div style="display:flex;gap:6px;margin-bottom:.8rem;flex-wrap:wrap">
    <button class="btn" id="sw-tab-request" onclick="switchTab('request',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Request a switch</button>
    <button class="btn" id="sw-tab-received" onclick="switchTab('received',this)">Received offers <span class="nav-badge">1</span></button>
    <button class="btn" id="sw-tab-history" onclick="switchTab('history',this)">History</button>
  </div>
  <!-- REQUEST -->
  <div id="sw-panel-request">
    <div class="card" style="max-width:500px">
      <div class="card-title">Propose a shift switch</div>
      <div class="field"><label>Your shift to give up</label>
        <select id="sw-my-shift" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
          <option value="s1">Mon Jun 23 · J1 Day (07:00–14:45) · Boys IA</option>
          <option value="s2">Sat Jun 28 · S1 Eve (15:00–22:45) · Boys IA</option>
          <option value="s3">Wed Jun 25 · N Night (22:30–07:00) · Boys IA</option>
        </select>
      </div>
      <div class="field"><label>Colleague to switch with</label>
        <select id="sw-colleague" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
          <option>Gilles Lezi</option><option>Eddy Bathalien</option><option>Greg Page</option><option>Angelo Kontakos</option><option>Jean Nicolas Michaud</option><option>Mark D'Agostino</option><option>Steven Yearwood</option>
        </select>
      </div>
      <div class="field"><label>Shift you want from them (optional — or leave blank to let them choose)</label>
        <input type="text" id="sw-want-shift" placeholder="e.g. Jun 24 · J1 Day · Boys IA — or leave blank">
      </div>
      <div class="field"><label>Note to colleague</label><textarea id="sw-note" rows="2" placeholder="e.g. Family commitment — can you cover my Monday?"></textarea></div>
      <button class="btn pri" style="width:100%" onclick="submitSwitchReq()">Send switch request to colleague</button>
    </div>
  </div>
  <!-- RECEIVED -->
  <div id="sw-panel-received" style="display:none">
    <div class="card">
      <div class="card-title">Switch offer received</div>
      <div style="background:var(--bluelight);border:1px solid #85B7EB;border-radius:var(--r);padding:12px;font-size:12px;margin-bottom:.8rem">
        <div style="font-weight:600;margin-bottom:4px">From: <b>Greg Page</b> <span style="color:var(--t3);font-weight:400">— Jun 20, 9:41 AM</span></div>
        <div>Greg is offering to switch: <b>his Wed Jun 25 · J1 Day</b> ↔ <b>your Sat Jun 28 · S1 Eve</b></div>
        <div style="color:var(--t3);margin-top:4px">"Would really help me out — my daughter's graduation is that evening."</div>
      </div>
      <div style="display:flex;gap:8px">
        <button class="btn" style="background:var(--green10);color:var(--green);border:1px solid var(--greenmid)" onclick="respondSwitch('accepted')">Accept — send to management</button>
        <button class="btn" style="background:var(--red10);color:#c0392b;border:1px solid #f5c6cb" onclick="respondSwitch('declined')">Decline</button>
      </div>
    </div>
  </div>
  <!-- HISTORY -->
  <div id="sw-panel-history" style="display:none">
    <table class="bt"><thead><tr><th>Your shift</th><th>Their shift</th><th>Colleague</th><th>Submitted</th><th>Status</th></tr></thead><tbody>
      <tr><td>Jun 3 · J1 · Boys IA</td><td>Jun 4 · S1 · Boys IA</td><td>Greg Page</td><td>May 30</td><td><span class="badge b-act">Approved</span></td></tr>
      <tr><td>May 7 · S1 · Boys IA</td><td>May 6 · J1 · Boys IA</td><td>Angelo Kontakos</td><td>May 4</td><td><span class="badge b-ter">Denied</span></td></tr>
    </tbody></table>
  </div>
</div>

<!-- duplicate removed — see p-emp-oncall below -->

<!-- ==================== MGMT: AVAILABILITY SHEETS ==================== -->
<div id="p-availability" class="page">
  <div style="display:flex;gap:6px;margin-bottom:1rem;flex-wrap:wrap">
    <button id="avmgmt-tab-pt" class="btn" onclick="availMgmtTab('pt',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">PT & Recall sheets</button>
    <button id="avmgmt-tab-ot" class="btn" onclick="availMgmtTab('ot',this)">OT availability sheets</button>
    <button id="avmgmt-tab-hist" class="btn" onclick="availMgmtTab('hist',this)">History by pay period</button>
  </div>

  <!-- PT & RECALL -->
  <div id="avmgmt-panel-pt">
    <div class="info">Part-time and Recall staff must submit every pay period. <b>Being marked available = obligation to work that shift.</b> Deadline: second-to-last Wednesday at 9:00 AM. Late = bottom of rotation. Non-compliant = management review.</div>
    <div class="card">
      <div class="card-title">PP 08 — PT & Recall submissions <span style="font-size:11px;color:var(--t3);font-weight:400">Deadline: Wed Jun 25 at 9:00 AM</span></div>
      <table class="bt" id="avail-pt-table"></table>
    </div>
  </div>

  <!-- OT AVAILABILITY -->
  <div id="avmgmt-panel-ot" style="display:none">
    <div class="info">Full-time staff only. Overtime availability is <b>never required</b> — it indicates willingness only. Used to build the OT offer list in seniority/fairness order.</div>
    <div class="card">
      <div class="card-title">PP 08 — OT availability submissions <span style="font-size:11px;color:var(--t3);font-weight:400">Deadline: Wed Jun 25 at 9:00 AM</span></div>
      <table class="bt" id="avail-ot-table"></table>
    </div>
  </div>

  <!-- HISTORY -->
  <div id="avmgmt-panel-hist" style="display:none">
    <div class="card">
      <div class="card-title">Availability history — select pay period
        <select id="avail-hist-pp" onchange="renderAvailHistory()" style="font-size:12px;padding:4px 8px;border-radius:var(--r);border:1px solid var(--bd2)">
          <option value="PP08">PP 08 (Jun 28 – Jul 11)</option>
          <option value="PP07">PP 07 (Jun 14–27)</option>
          <option value="PP06">PP 06 (May 31–Jun 13)</option>
        </select>
      </div>
      <table class="bt" id="avail-hist-table"></table>
    </div>
  </div>
</div>

<!-- ==================== MGMT: ON-CALL ==================== -->
<div id="p-oncall" class="page">
  <div class="info">⏰ On-call hours: <b>5:00 PM – 9:00 AM</b> (outside scheduler office hours). The on-call manager handles book-offs and emergency replacements during these hours. Schedule edits made here are live immediately; staff see the update only when the scheduler pushes Mon/Wed/Fri.</div>
  <div style="display:flex;gap:6px;margin-bottom:1rem;flex-wrap:wrap">
    <button id="oncall-tab-pkg" class="btn" onclick="oncallTab('pkg',this)" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Replacement package</button>
    <button id="oncall-tab-bookoffs" class="btn" onclick="oncallTab('bookoffs',this)">Book-off requests <span class="nav-badge" style="margin-left:4px">1</span></button>
  </div>

  <!-- REPLACEMENT PACKAGE -->
  <div id="oncall-panel-pkg">
    <div class="card">
      <div class="card-title">Select shift to fill — on-call package</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:1rem">
        <select id="oncall-shift-select" onchange="renderOncallPackage()" style="font-size:12px;padding:6px 10px;border-radius:var(--r);border:1px solid var(--bd2)">
          <option value="">— Select shift —</option>
          <option value="sat-s1">Sat Jun 20 · S1 Eve (15:00–22:45) · Boys IA</option>
          <option value="fri-n">Fri Jun 20 · N Night (22:30–07:00) · Girls IA</option>
          <option value="wed-j1">Wed Jun 25 · J1 Day (07:00–14:45) · Boys IA</option>
        </select>
      </div>
      <div id="oncall-package-table"></div>
    </div>
    <div class="card">
      <div class="card-title">Add name to shift</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div class="field" style="margin:0;flex:1;min-width:160px"><label>Employee</label><select id="oncall-add-emp" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%"><option>Keith Burnett</option><option>Kerwin Guy-Roach</option><option>Ansonia Arrington</option><option>Steven Yearwood</option><option>Keon Pompey</option><option>Gilles Lezi</option><option>Jema Larose</option><option>Chynna Lewis</option><option>Greg Page</option></select></div>
        <div class="field" style="margin:0;flex:1;min-width:140px"><label>Shift</label><select id="oncall-add-shift" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%"><option>Sat Jun 20 · S1 · Boys IA</option><option>Fri Jun 20 · N · Girls IA</option><option>Wed Jun 25 · J1 · Boys IA</option></select></div>
        <button class="btn pri" onclick="addToShift()">Add to shift</button>
      </div>
    </div>
  </div>

  <!-- BOOK-OFF REQUESTS -->
  <div id="oncall-panel-bookoffs" style="display:none">
    <div class="card">
      <div class="card-title">Pending book-off requests</div>
      <table class="bt" id="oncall-bookoff-table"></table>
    </div>
    <div class="card">
      <div class="card-title">Book-off history — current pay period</div>
      <table class="bt" id="oncall-bookoff-hist"></table>
    </div>
  </div>
</div>

<!-- ==================== MGMT: SHIFT ROSTER ==================== -->
<div id="p-roster" class="page">
  <div class="info">🔒 Management view only. Add or remove employees from the master roster. Assign names to shifts for coverage tracking. Staff do not see rotation order.</div>
  <div class="grid2">
    <div class="card">
      <div class="card-title">Master employee roster
        <button class="btn sm pri" onclick="openModal('add-roster-modal')">+ Add employee</button>
      </div>
      <table class="bt" id="roster-emp-table"></table>
    </div>
    <div class="card">
      <div class="card-title">Shift coverage log
        <button class="btn sm" onclick="openModal('add-coverage-modal')">+ Add coverage</button>
      </div>
      <table class="bt" id="roster-coverage-table"></table>
    </div>
  </div>
</div>

<!-- ==================== MGMT: DEADLINES & MEMOS ==================== -->
<div id="p-deadlines" class="page">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.8rem">
    <div style="font-size:12px;color:var(--t2)">Scheduling reminders, deadline notices, and important notices visible to all staff.</div>
    <button class="btn pri" onclick="openModal('new-deadline-modal')">+ Add reminder</button>
  </div>
  <div id="deadline-list"></div>
</div>

<!-- ==================== MGMT: WEEKLY SUMMARY ==================== -->
<div id="p-weeklysummary" class="page">
  <div class="info">Weekly summary emails are automatically sent to Scheduling Admin and Management every <b>Sunday at 20:00</b>, covering the full week's schedule activity. Content is editable before send.</div>
  <div class="card">
    <div class="card-title">Week of Jun 14–20, 2026 — summary preview <button class="btn sm pri" onclick="notify('Weekly summary email sent to all management and scheduling contacts.')">Send now</button></div>
    <div style="background:var(--bg1);border-radius:var(--r);padding:1rem;font-size:12px;line-height:1.7">
      <div style="font-weight:700;margin-bottom:.5rem;font-size:13px">📋 UTHC Scheduling — Weekly Summary · Jun 14–20, 2026</div>
      <div style="color:var(--t2);margin-bottom:.75rem;font-size:11px">Auto-generated · Sent to: Scheduling Admin, On-call Manager, Unit Managers</div>
      <div style="font-weight:600;margin-bottom:3px">Book-offs (4)</div>
      <div>• Eddy Bathalien — Jun 14, Jun 19 (Stat) — <span style="color:var(--green)">Approved</span></div>
      <div>• Shannon Ridley — Jun 17 (Vacation) — <span style="color:var(--green)">Approved</span></div>
      <div>• Paul Vincent — Jun 19 (Vacation) — <span style="color:var(--amber)">Pending</span></div>
      <div style="font-weight:600;margin:.65rem 0 3px">Overtime assigned (3)</div>
      <div>• Keith Burnett — Jun 22 (ESC / Montreal) — Accepted 8:14 AM</div>
      <div>• Greg Page — Jun 15 (OT cover Boys Ed.) — Accepted 9:02 AM</div>
      <div>• Gilles Lezi — Jun 20 (S1 cover) — <span style="color:var(--amber)">Pending offer</span></div>
      <div style="font-weight:600;margin:.65rem 0 3px">Shift switches approved (1)</div>
      <div>• Kerwin Guy-Roach ↔ Wesley Thomas — Jun 23 ↔ Jun 24 (Girls Educators)</div>
      <div style="font-weight:600;margin:.65rem 0 3px">Schedule updates published</div>
      <div>• Mon Jun 16 at 8:00 AM — Coverage updates Boys IA Week 2</div>
      <div>• Wed Jun 18 at 8:00 AM — OT additions Boys Educators</div>
      <div>• Fri Jun 20 at 8:00 AM — Final Week 2 + Week 3 preview</div>
      <div style="font-weight:600;margin:.65rem 0 3px">Unfilled shifts (2)</div>
      <div>• Boys Educators — Sat Jun 20, S1 (active OT offer)</div>
      <div>• Girls IA — Fri Jun 20, N (CNR — management notified)</div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">Schedule update log — PP 07 / PP 08
      <button class="btn pri" onclick="pushScheduleUpdate()">📤 Send schedule update now</button>
    </div>
    <div class="info" style="margin-bottom:.75rem">Updates are normally pushed <b>Monday, Wednesday, and Friday</b>. Click "Send schedule update now" to notify all staff and timestamp the push. On-call managers can edit the schedule live at any time — staff see changes only at the next push.</div>
    <table class="bt" id="sched-push-log"></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: AVAILABILITY (PT & RECALL) ==================== -->
<div id="p-emp-availability" class="page">
  <div class="info">📋 <b>Part-time & Recall staff.</b> Submit your availability for the upcoming pay period. <b>Being available = you are required to work that shift.</b> Deadline: every second-to-last Wednesday at 9:00 AM. Late = accepted but placed at <b>bottom of rotation</b>. Non-compliant = management review.</div>
  <div class="card" style="max-width:560px">
    <div class="card-title">PP 08 — Availability submission <span style="font-size:11px;color:var(--red);font-weight:400">Deadline: Wed Jun 25 at 9:00 AM</span></div>
    <div class="info" style="margin-bottom:.8rem">Minimum: <b>Recall</b> — 4 shifts incl. 2 weekend (Sat+Sun) + 1 eve weekend. <b>PT block</b> — 4 shifts incl. 2 weekend shifts.</div>
    <div style="display:flex;gap:8px;margin-bottom:.85rem">
      <button class="btn" onclick="setAvailMethod('upload',this)" id="av-upload-btn" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Upload sheet</button>
      <button class="btn" onclick="setAvailMethod('digital',this)" id="av-digital-btn">Fill in app</button>
    </div>
    <div id="av-upload-area">
      <div style="border:2px dashed var(--bd2);border-radius:var(--r);padding:1.5rem;text-align:center;font-size:12px;color:var(--t2);margin-bottom:.8rem">
        <div style="font-size:22px;margin-bottom:6px">📎</div>
        <div>Drag your availability sheet here, or</div>
        <label style="color:var(--blue);cursor:pointer;font-weight:600"> click to upload <input type="file" style="display:none" accept=".pdf,.xlsx,.csv,.png,.jpg" onchange="handleAvailUpload(this)"></label>
        <div style="font-size:10px;color:var(--t3);margin-top:4px">PDF, Excel, image accepted</div>
      </div>
    </div>
    <div id="av-digital-area" style="display:none">
      <div style="font-size:11px;font-weight:600;color:var(--t2);margin-bottom:6px">Mark your available shifts — ✓ = available (you are required to work if offered)</div>
      <div style="overflow-x:auto"><table class="bt" id="avail-grid-table"></table></div>
    </div>
    <button class="btn pri" style="width:100%;margin-top:.6rem" onclick="submitAvailability('pt')">Submit availability sheet</button>
  </div>
  <div class="card" style="max-width:560px">
    <div class="card-title">My submission history</div>
    <table class="bt"><thead><tr><th>Pay period</th><th>Submitted</th><th>Status</th><th>Note</th></tr></thead><tbody>
      <tr><td>PP 07 (Jun 14–27)</td><td>Jun 3 at 8:47 AM</td><td><span class="badge b-act">On time</span></td><td>Compliant — normal rotation</td></tr>
      <tr><td>PP 06 (May 31–Jun 13)</td><td>May 20 at 9:41 AM</td><td><span class="badge b-act">On time</span></td><td>Compliant — normal rotation</td></tr>
      <tr><td>PP 05 (May 17–30)</td><td>May 8 at 11:02 AM</td><td><span class="badge b-sus">Late</span></td><td>Placed at bottom of rotation for PP 05</td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: OT AVAILABILITY (FT ONLY) ==================== -->
<div id="p-emp-ot-avail" class="page">
  <div class="info">⏱ <b>Full-time staff — Overtime availability.</b> This sheet is optional. Indicating availability does <b>not</b> obligate you to work. It is used to build the OT offer list in seniority/fairness order. Deadline: same as regular availability sheet.</div>
  <div class="card" style="max-width:560px">
    <div class="card-title">PP 08 — OT availability submission <span style="font-size:11px;color:var(--t3);font-weight:400">Optional · Deadline: Wed Jun 25</span></div>
    <div style="display:flex;gap:8px;margin-bottom:.85rem">
      <button class="btn" onclick="setOtAvailMethod('upload',this)" id="ot-upload-btn" style="background:var(--bluelight);color:var(--blue);border-color:#85B7EB">Upload sheet</button>
      <button class="btn" onclick="setOtAvailMethod('digital',this)" id="ot-digital-btn">Fill in app</button>
    </div>
    <div id="ot-upload-area">
      <div style="border:2px dashed var(--bd2);border-radius:var(--r);padding:1.5rem;text-align:center;font-size:12px;color:var(--t2);margin-bottom:.8rem">
        <div style="font-size:22px;margin-bottom:6px">📎</div>
        <div>Drag your OT availability sheet here, or</div>
        <label style="color:var(--blue);cursor:pointer;font-weight:600"> click to upload <input type="file" style="display:none" accept=".pdf,.xlsx,.csv,.png,.jpg" onchange="handleOtUpload(this)"></label>
        <div style="font-size:10px;color:var(--t3);margin-top:4px">PDF, Excel, image accepted</div>
      </div>
    </div>
    <div id="ot-digital-area" style="display:none">
      <div style="font-size:11px;font-weight:600;color:var(--t2);margin-bottom:6px">Mark shifts you are willing to work OT — management will contact you in order</div>
      <div style="overflow-x:auto"><table class="bt" id="ot-avail-grid-table"></table></div>
    </div>
    <button class="btn pri" style="width:100%;margin-top:.6rem" onclick="submitAvailability('ot')">Submit OT availability sheet</button>
  </div>
  <div class="card" style="max-width:560px">
    <div class="card-title">My OT availability history</div>
    <table class="bt"><thead><tr><th>Pay period</th><th>Submitted</th><th>Status</th></tr></thead><tbody>
      <tr><td>PP 07 (Jun 14–27)</td><td>Jun 3 at 9:15 AM</td><td><span class="badge b-act">Submitted</span></td></tr>
      <tr><td>PP 06 (May 31–Jun 13)</td><td>—</td><td><span class="badge" style="background:var(--bg1);color:var(--t2)">Not submitted</span></td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: ON-CALL INFO ==================== -->
<div id="p-emp-oncall" class="page">
  <div class="info">📞 On-call hours are <b>5:00 PM – 9:00 AM</b> daily (outside scheduler office hours). During these hours, the on-call manager handles all book-offs and emergency replacements. <b>You must also call the manager directly</b> when submitting a book-off — the app submission alone is not sufficient.</div>
  <div class="card" style="max-width:420px">
    <div class="card-title">On-call manager — current week</div>
    <div style="padding:.75rem 0">
      <div style="font-size:15px;font-weight:700;margin-bottom:4px">🧑‍💼 Sandra Beaumont</div>
      <div style="font-size:12px;color:var(--t2);margin-bottom:2px">📞 (514) 555-0192</div>
      <div style="font-size:12px;color:var(--t2);margin-bottom:.75rem">On-call: Mon Jun 16 – Sun Jun 22</div>
      <div class="info" style="margin:0">Schedule updates made during on-call hours are <b>live for management</b> immediately. You will see changes in your schedule when the scheduler publishes the next update (Mon / Wed / Fri).</div>
    </div>
  </div>
</div>

<!-- ==================== MGMT: STAFF PROFILES ==================== -->
<div id="p-empprofile" class="page">
  <div class="info">🔒 Management view only. Click any employee to view their full activity summary for the current pay period.</div>
  <div style="display:flex;gap:8px;margin-bottom:.8rem;flex-wrap:wrap">
    <input type="text" id="profile-search" placeholder="Search employee..." oninput="filterProfileList()" style="padding:7px 10px;border-radius:var(--r);border:1px solid var(--bd2);font-size:12px;flex:1;min-width:160px">
  </div>
  <div id="profile-list-view">
    <div class="card">
      <div class="card-title">All staff — click to view profile</div>
      <table class="bt" id="profile-emp-table"></table>
    </div>
  </div>
  <div id="profile-detail-view" style="display:none">
    <button class="btn sm" onclick="document.getElementById('profile-list-view').style.display='';document.getElementById('profile-detail-view').style.display='none'" style="margin-bottom:.8rem">← Back to list</button>
    <div id="profile-detail-content"></div>
  </div>
</div>

<!-- ==================== MGMT: LOAN OF SERVICE ==================== -->
<div id="p-loanservice" class="page">
  <div class="info">A loan of service occurs when a northern unit requests UTHC staff for 4+ weeks in a specific community. The loaned employee is <b>removed from the UTHC schedule</b> for the full duration. A notification is sent to the employee, scheduler, and management.</div>
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.8rem">
    <span style="font-size:12px;color:var(--t2)">Active and past loan placements.</span>
    <button class="btn pri" onclick="openModal('new-loan-modal')">+ New loan of service</button>
  </div>
  <div id="loan-list"></div>
</div>

<!-- ==================== MGMT: REGULAR CONTACT LOG ==================== -->
<div id="p-regularcontact" class="page">
  <div class="info">Use this log when calling PT or Recall staff to fill a <b>regular (non-OT)</b> shift. Track who was contacted, at what time, and their response. Once someone is passed over, the app indicates who was moved to next.</div>
  <div class="card">
    <div class="card-title">Regular shift — contact chain
      <button class="btn sm pri" onclick="openModal('new-regcontact-modal')">+ New contact chain</button>
    </div>
    <table class="bt" id="regcontact-table"></table>
  </div>
</div>

<!-- ==================== MGMT: DROP SHIFT REQUESTS ==================== -->
<div id="p-dropshiftmgmt" class="page">
  <div class="info">Employees can request to drop a shift. Block/regular shifts require a leave code. PT/Recall non-block and OT pickup shifts require no reason. Review and approve or deny below.</div>
  <div class="card">
    <div class="card-title">Pending drop requests</div>
    <table class="bt" id="drop-mgmt-table"></table>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">Drop request history — PP 08</div>
    <table class="bt" id="drop-hist-table"></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: DROP A SHIFT ==================== -->
<!-- ==================== EMPLOYEE: NEGOTIATE SHIFTS ==================== -->
<div id="p-emp-negtimes" class="page">
  <div class="info">If you can partially cover an unfilled shift — arriving early, leaving late, or covering a portion — submit a negotiated time request here. Management will review and confirm your adjusted hours if the coverage works.</div>
  <div class="card" style="max-width:480px">
    <div class="card-title">Submit a partial coverage offer</div>
    <div class="field"><label>Unfilled shift</label>
      <select style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
        <option>Sat Oct 25 · J1 Day (07:00–14:45) · Boys IA — book-off coverage needed</option>
        <option>Wed Oct 22 · S1 Evening (15:00–22:45) · Girls Educators — CNR</option>
        <option>Mon Oct 20 · N Night (22:30–07:00) · Boys IA — recall needed</option>
      </select>
    </div>
    <div class="field"><label>Hours I can cover — start</label><input type="time" value="10:00"></div>
    <div class="field"><label>Hours I can cover — end</label><input type="time" value="14:45"></div>
    <div class="field"><label>Notes (optional)</label><input type="text" placeholder="e.g. Can stay until end of shift if needed"></div>
    <button class="btn pri" onclick="notify('Partial coverage offer submitted — management will review and confirm.')">Submit offer</button>
  </div>
  <div class="card" style="margin-top:.8rem">
    <div class="card-title">My submitted offers</div>
    <table class="bt"><thead><tr><th>Shift</th><th>Offered hours</th><th>Status</th></tr></thead><tbody>
      <tr>
        <td>Tue Oct 21 · S1 Evening · Boys IA</td>
        <td>17:00 – 22:45</td>
        <td><span class="badge" style="background:#FFF8E1;color:#B8860B">Pending review</span></td>
      </tr>
    </tbody></table>
  </div>
</div>

<div id="p-emp-dropshift" class="page">
  <div class="info">You can request to drop a shift here. <b>Regular block shifts (FT/PT)</b> require a leave code (Vac/Stat/Sick/etc.). <b>PT or Recall non-block shifts and OT pickups</b> do not require a reason. Management will review all requests.</div>
  <div class="card" style="max-width:480px">
    <div class="card-title">Request to drop a shift</div>
    <div class="field"><label>Shift to drop</label>
      <select id="drop-shift-sel" onchange="checkDropCode()" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
        <option value="block">Mon Jun 23 · J1 Day (07:00–14:45) · Boys IA [Block shift]</option>
        <option value="pickup">Sat Jun 20 · S1 Eve (15:00–22:45) · Boys IA [OT pickup]</option>
        <option value="nonblock">Wed Jun 25 · N Night (22:30–07:00) · Girls IA [Non-block]</option>
      </select>
    </div>
    <div id="drop-code-area">
      <div class="info" style="margin:.6rem 0">This is a <b>block/regular shift</b> — a leave code is required.</div>
      <div class="field"><label>Leave code <span style="color:var(--red)">* required</span></label>
        <div class="ltabs">
          <div class="ltab" onclick="selDropLeave(this,'Vacation')">Vacation</div>
          <div class="ltab" onclick="selDropLeave(this,'Sick')">Sick</div>
          <div class="ltab" onclick="selDropLeave(this,'Stat')">Stat</div>
          <div class="ltab" onclick="selDropLeave(this,'LIB')">LIB</div>
          <div class="ltab" onclick="selDropLeave(this,'Psychosocial')">Psychosocial</div>
        </div>
        <input type="hidden" id="drop-leave-code" value="">
      </div>
    </div>
    <div id="drop-noreason-area" style="display:none">
      <div class="info" style="margin:.6rem 0">No leave code required for this shift type. You may add an optional note.</div>
    </div>
    <div class="field"><label>Additional notes (optional)</label><input type="text" id="drop-notes" placeholder="Any details for management..."></div>
    <button class="btn pri" style="width:100%;margin-top:.4rem" onclick="submitDropShift()">Submit drop request</button>
  </div>
  <div class="card" style="max-width:480px;margin-top:.8rem">
    <div class="card-title">My drop request history</div>
    <table class="bt"><thead><tr><th>Shift</th><th>Code</th><th>Submitted</th><th>Status</th></tr></thead><tbody>
      <tr><td>Jun 3 · J1 · Boys IA</td><td>Vacation</td><td>May 28</td><td><span class="badge b-act">Approved</span></td></tr>
      <tr><td>May 17 · S1 · Boys IA</td><td>Sick</td><td>May 16</td><td><span class="badge b-act">Approved</span></td></tr>
    </tbody></table>
  </div>
</div>

<!-- ==================== EMPLOYEE: NOTIFICATIONS ==================== -->
<div id="p-emp-notifications" class="page">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.8rem">
    <div style="font-size:12px;color:var(--t2)">In-app notifications for schedule updates, shift assignments, memos, and loan of service requests.</div>
    <button class="btn sm" onclick="markAllRead()">Mark all read</button>
  </div>
  <div id="notif-inbox"></div>
</div>

</div><!-- .main -->

<!-- MODALS -->
<div id="new-memo-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">New memo <span class="mx" onclick="closeModal('new-memo-modal')">×</span></div>
    <div class="field"><label>Memo type</label><select id="m-type"><option value="escort">Northern escort</option><option value="transport">Transportation shift</option></select></div>
    <div class="row2">
      <div class="field"><label>Staff assigned</label><input id="m-staff" type="text" placeholder="e.g. Mark D'Agostino"></div>
      <div class="field"><label>Date</label><input id="m-date" type="date"></div>
    </div>
    <div class="row2">
      <div class="field"><label>Number of youth</label><input id="m-youth" type="number" min="1" placeholder="e.g. 2"></div>
      <div class="field"><label>Destination / community</label><input id="m-dest" placeholder="e.g. Kuujjuaq"></div>
    </div>
    <div class="row2">
      <div class="field"><label>Start time</label><input id="m-start" type="time"></div>
      <div class="field"><label>End time</label><input id="m-end" type="time"></div>
    </div>
    <div class="field"><label>Notes</label><textarea id="m-notes" rows="2" placeholder="Any additional details..."></textarea></div>
    <button class="btn pri" style="width:100%" onclick="saveMemo()">Save memo</button>
  </div>
</div>

<div id="new-leave-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Add leave record <span class="mx" onclick="closeModal('new-leave-modal')">×</span></div>
    <div class="row2">
      <div class="field"><label>Employee</label><input type="text" placeholder="Name"></div>
      <div class="field"><label>Leave type</label><select><option>Sick leave</option><option>Maternity leave</option><option>Paternity leave</option><option>CNESST leave</option><option>Vacation</option><option>Other</option></select></div>
    </div>
    <div class="row2">
      <div class="field"><label>Date started</label><input type="date"></div>
      <div class="field"><label>Expected return</label><input type="date"></div>
    </div>
    <div class="field"><label>Progressive return?</label><select id="prog-sel" onchange="document.getElementById('prog-detail').style.display=this.value==='yes'?'block':'none'"><option value="no">No</option><option value="yes">Yes</option></select></div>
    <div class="field" id="prog-detail" style="display:none"><label>Progressive return schedule</label><input type="text" placeholder="e.g. 2 shifts/week for 2 weeks, then full schedule"></div>
    <button class="btn pri" style="width:100%" onclick="closeModal('new-leave-modal');notify('Leave record saved. Visible to management only.')">Save record</button>
  </div>
</div>

<div id="tran-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title"><span id="tran-title">Transport/escort detail</span><span class="mx" onclick="closeModal('tran-modal')">×</span></div>
    <div id="tran-body" class="memo-grid"></div>
    <button class="btn" style="width:100%;margin-top:.8rem" onclick="closeModal('tran-modal')">Close</button>
  </div>
</div>

<div id="denied-modal" class="modal-wrap">
  <div class="modal">
    <div class="deny-screen"><div class="deny-icon">🔒</div><div style="font-weight:600;margin-bottom:4px">Access restricted</div><div style="font-size:12px;color:var(--t2)">This transport/escort detail is only visible to the assigned employee and management.</div></div>
    <button class="btn" style="width:100%;margin-top:.5rem" onclick="closeModal('denied-modal')">Close</button>
  </div>
</div>

<!-- CELL EDIT MODAL -->
<div id="cell-edit-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Edit shift cell <span class="mx" onclick="closeModal('cell-edit-modal')">×</span></div>
    <div id="cell-edit-info" style="background:var(--bluelight);border-radius:var(--r);padding:9px 12px;font-size:12px;margin-bottom:.8rem;color:var(--bluedark)"></div>
    <div class="row2">
      <div class="field"><label>Custom start time</label><input type="time" id="cell-start"></div>
      <div class="field"><label>Custom end time</label><input type="time" id="cell-end"></div>
    </div>
    <div class="field"><label>Shift type</label>
      <select id="cell-shifttype" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%" onchange="cellShiftTypeChange(this)">
        <option value="">— Keep existing —</option>
        <optgroup label="Day shifts">
          <option value="J1">J1 — Day 1</option>
          <option value="J2">J2 — Day 2</option>
          <option value="J3">J3 — Day 3</option>
        </optgroup>
        <optgroup label="Evening shifts">
          <option value="S1">S1 — Evening 1</option>
          <option value="S2">S2 — Evening 2</option>
          <option value="S3">S3 — Evening 3</option>
        </optgroup>
        <optgroup label="Double shifts">
          <option value="J/S">J/S — Double (Day + Evening)</option>
          <option value="J1/S1">J1/S1 — Double (J1 + S1)</option>
          <option value="J2/S2">J2/S2 — Double (J2 + S2)</option>
        </optgroup>
        <optgroup label="Overtime">
          <option value="OT·J1">OT·J1 — OT on Day shift</option>
          <option value="OT·J2">OT·J2 — OT on Day 2</option>
          <option value="OT·S1">OT·S1 — OT on Evening shift</option>
          <option value="OT·S2">OT·S2 — OT on Evening 2</option>
          <option value="OT·N">OT·N — OT on Night</option>
        </optgroup>
        <optgroup label="Other">
          <option value="N">N — Night</option>
          <option value="R">R — Rest day</option>
          <option value="__custom__">Other — type below ↓</option>
        </optgroup>
      </select>
      <input type="text" id="cell-shifttype-custom" placeholder="e.g. J1/T, OT·S3, J4, or any code" style="display:none;margin-top:6px;font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%;box-sizing:border-box">
    </div>
    <div class="field"><label>Replacement / coverage — staff name</label>
      <select id="cell-empname" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%" onchange="cellNameSelectChange(this)">
        <option value="">— None —</option>
        <optgroup label="Intervention Agents">
          <option>Keith</option>
          <option>Mark</option>
          <option>Greg</option>
          <option>Jean-Nicolas</option>
          <option>Angelo</option>
          <option>Tracy</option>
          <option>Jema</option>
          <option>Mahkeda</option>
          <option>Steven</option>
          <option>Keon</option>
          <option>Errol</option>
          <option>Darlene</option>
        </optgroup>
        <optgroup label="Educators">
          <option>Gilles</option>
          <option>Eddy</option>
          <option>Makeda</option>
          <option>Kerwin</option>
          <option>Ansonia</option>
          <option>Yvonne</option>
          <option>Shannon</option>
        </optgroup>
        <optgroup label="Agency / Other">
          <option value="__agency__">Agency / outsourced staff — type name below ↓</option>
          <option>On-call</option>
        </optgroup>
      </select>
      <input type="text" id="cell-empname-custom" placeholder="Type agency or new staff name (add * for agency)" style="display:none;margin-top:6px;font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%;box-sizing:border-box">
    </div>
    <div class="field"><label>Leave / book-off code (if applicable)</label>
      <select id="cell-code">
        <option value="">— None —</option>
        <option value="VAC">VAC — Vacation</option>
        <option value="SICK">SICK — Sick leave</option>
        <option value="STAT">STAT — Statutory holiday</option>
        <option value="PSYCH">PSYCH — Psychological day</option>
        <option value="TRAINING">TRAINING — Training</option>
        <option value="PEXT">PEXT — Bank time</option>
        <option value="OT-TAKEN">OT-TAKEN — OT taken</option>
        <option value="AUTHO">AUTHO — Authorized without pay</option>
        <option value="CNESST">CNESST — Work injury</option>
        <option value="MAT">MAT — Maternity leave</option>
        <option value="LOAN">LOAN — On loan of service</option>
      </select>
    </div>
    <div class="info" style="font-size:11px">Changes are live for management immediately. Employees see the update at the next Mon/Wed/Fri schedule push.</div>
    <div style="display:flex;gap:8px;margin-top:.2rem">
      <button class="btn pri" style="flex:1" onclick="saveCellEdit()">Save changes</button>
      <button class="btn" style="flex:0 0 auto;color:#c0392b;border-color:#f5c6cb" onclick="removeCellShift()" title="Remove this shift entirely">🗑 Remove shift</button>
    </div>
  </div>
</div>

<!-- ADD SENIORITY MODAL -->
<div id="add-sen-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Add staff to seniority list <span class="mx" onclick="closeModal('add-sen-modal')">×</span></div>
    <div class="row2">
      <div class="field"><label>Full name</label><input type="text" id="sen-new-name" placeholder="e.g. Maria Santos"></div>
      <div class="field"><label>Job title</label>
        <select id="sen-new-title">
          <option value="ed">Educator</option>
          <option value="ed2">Senior Educator</option>
          <option value="ia">Intervention Agent</option>
          <option value="ia2">Senior Intervention Agent</option>
        </select>
      </div>
    </div>
    <div class="row2">
      <div class="field"><label>Position type</label>
        <select id="sen-new-pos"><option value="FT">Full-time (FT)</option><option value="TFT">Temp FT (TFT)</option><option value="PT">Part-time (PT)</option><option value="Recall">Recall</option></select>
      </div>
      <div class="field"><label>Seniority start date</label><input type="date" id="sen-new-date"></div>
    </div>
    <div class="field"><label>Unit</label>
      <select id="sen-new-unit"><option>Boys</option><option>Girls</option><option>Both</option></select>
    </div>
    <button class="btn pri" style="width:100%" onclick="addSenStaff()">Add to list</button>
  </div>
</div>

<!-- LOAN OF SERVICE MODAL -->
<div id="new-loan-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">New loan of service <span class="mx" onclick="closeModal('new-loan-modal')">×</span></div>
    <div class="field"><label>Employee being loaned</label>
      <select id="loan-emp" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
        <option>Keith Burnett</option><option>Kerwin Guy-Roach</option><option>Ansonia Arrington</option><option>Greg Page</option><option>Gilles Lezi</option>
      </select>
    </div>
    <div class="row2">
      <div class="field"><label>Requesting community / unit</label><input type="text" id="loan-community" placeholder="e.g. Kuujjuaq Health Center"></div>
      <div class="field"><label>Duration (weeks)</label><input type="number" id="loan-weeks" min="4" placeholder="e.g. 6" value="4"></div>
    </div>
    <div class="row2">
      <div class="field"><label>Start date</label><input type="date" id="loan-start"></div>
      <div class="field"><label>End date (estimated)</label><input type="date" id="loan-end"></div>
    </div>
    <div class="field"><label>Notes / purpose</label><textarea id="loan-notes" rows="2" placeholder="e.g. Requested to support youth crisis unit during staffing shortage"></textarea></div>
    <div class="info" style="font-size:11px">The employee will be removed from the UTHC schedule for this entire period. Notifications sent to employee, scheduler, and management on save.</div>
    <button class="btn pri" style="width:100%" onclick="saveLoan()">Confirm loan of service</button>
  </div>
</div>

<!-- REGULAR CONTACT MODAL -->
<div id="new-regcontact-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Start regular shift contact chain <span class="mx" onclick="closeModal('new-regcontact-modal')">×</span></div>
    <div class="field"><label>Shift to fill</label><input type="text" id="rc-shift" placeholder="e.g. Sat Jun 20 · S1 (15:00–22:45) · Boys IA"></div>
    <div class="field"><label>Reason shift is open</label><input type="text" id="rc-reason" placeholder="e.g. Book-off — Paul Vincent"></div>
    <button class="btn pri" style="width:100%" onclick="startRegContact()">Create contact chain</button>
  </div>
</div>

<!-- ROSTER MODALS -->
<div id="add-roster-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Add employee to roster <span class="mx" onclick="closeModal('add-roster-modal')">×</span></div>
    <div class="row2">
      <div class="field"><label>Full name</label><input type="text" id="roster-name" placeholder="e.g. Chynna Lewis"></div>
      <div class="field"><label>Position type</label><select id="roster-pos"><option value="FT">Full-time (FT)</option><option value="TFT">Temp FT (TFT)</option><option value="PT">Part-time (PT)</option><option value="Recall">Recall</option></select></div>
    </div>
    <div class="row2">
      <div class="field"><label>Unit</label><select id="roster-unit"><option>Boys IA</option><option>Girls IA</option><option>Boys Educators</option><option>Girls Educators</option></select></div>
      <div class="field"><label>Seniority date</label><input type="date" id="roster-sendate"></div>
    </div>
    <button class="btn pri" style="width:100%" onclick="saveRosterEmp()">Add to roster</button>
  </div>
</div>
<div id="add-coverage-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Add shift coverage <span class="mx" onclick="closeModal('add-coverage-modal')">×</span></div>
    <div class="field"><label>Employee name</label><select id="cov-emp" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%"><option>Keith Burnett</option><option>Kerwin Guy-Roach</option><option>Ansonia Arrington</option><option>Steven Yearwood</option><option>Keon Pompey</option><option>Gilles Lezi</option><option>Jema Larose</option><option>Chynna Lewis</option><option>Greg Page</option></select></div>
    <div class="row2">
      <div class="field"><label>Date</label><input type="date" id="cov-date"></div>
      <div class="field"><label>Shift</label><select id="cov-shift"><option>J1 — Day (07:00–14:45)</option><option>S1 — Eve (15:00–22:45)</option><option>N — Night (22:30–07:00)</option></select></div>
    </div>
    <div class="field"><label>Unit</label><select id="cov-unit"><option>Boys IA</option><option>Girls IA</option><option>Boys Educators</option><option>Girls Educators</option></select></div>
    <div class="field"><label>Notes (optional)</label><input type="text" id="cov-notes" placeholder="e.g. OT cover, book-off replacement"></div>
    <button class="btn pri" style="width:100%" onclick="saveCoverage()">Add coverage record</button>
  </div>
</div>

<div id="new-genmemo-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">New general memo <span class="mx" onclick="closeModal('new-genmemo-modal')">×</span></div>
    <div class="field"><label>Subject</label><input type="text" id="gm-subject" placeholder="e.g. Reminder: PP 08 schedule published"></div>
    <div class="field"><label>Send to</label>
      <select id="gm-to"><option>All staff</option><option>Boys unit only</option><option>Girls unit only</option><option>Educators only</option><option>Intervention Agents only</option><option>Management only</option></select>
    </div>
    <div class="field"><label>Message</label><textarea id="gm-body" rows="4" placeholder="Type your memo here..."></textarea></div>
    <div class="field"><label>Priority</label>
      <select id="gm-priority"><option>Normal</option><option>Important</option><option>Urgent</option></select>
    </div>
    <button class="btn pri" style="width:100%" onclick="sendGenMemo()">Send memo</button>
  </div>
</div>

<div id="negtime-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Submit partial cover times <span class="mx" onclick="closeModal('negtime-modal')">×</span></div>
    <div id="negtime-shift-info" style="background:var(--amberlight);border-radius:var(--r);padding:9px 12px;font-size:12px;margin-bottom:.8rem;color:var(--amber)"></div>
    <div class="info">Enter the hours you are able to cover. Management will review and approve or deny your request.</div>
    <div class="row2">
      <div class="field"><label>I can arrive at</label><input type="time" id="neg-arrive"></div>
      <div class="field"><label>I need to leave by</label><input type="time" id="neg-leave"></div>
    </div>
    <div class="field"><label>Notes (optional)</label><input type="text" id="neg-notes" placeholder="e.g. Can stay later if needed, have a ride at 23:00"></div>
    <button class="btn pri" style="width:100%" onclick="submitNegTime()">Submit for management approval</button>
  </div>
</div>

<!-- TRAN/ESC EDIT MODAL -->
<div id="tranesc-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title" id="tranesc-modal-title">Add Transport / Escort entry <span class="mx" onclick="closeModal('tranesc-modal')">×</span></div>
    <input type="hidden" id="tranesc-edit-idx" value="-1">
    <input type="hidden" id="tranesc-edit-pp" value="0">
    <input type="hidden" id="tranesc-edit-day" value="0">
    <div class="field"><label>Type</label>
      <select id="tranesc-type" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
        <option value="TRAN">TRAN — Transport</option>
        <option value="ESC">ESC — Escort</option>
      </select>
    </div>
    <div class="field"><label>Staff assigned</label>
      <select id="tranesc-staff" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%" onchange="tranEscStaffChange(this)">
        <option value="">— Select staff —</option>
        <optgroup label="Intervention Agents">
          <option>Keith</option><option>Mark</option><option>Greg</option>
          <option>Jean-Nicolas</option><option>Angelo</option><option>Tracy</option>
          <option>Jema</option><option>Mahkeda</option><option>Steven</option>
          <option>Keon</option><option>Errol</option><option>Darlene</option><option>Chris</option>
        </optgroup>
        <optgroup label="Agency / Other">
          <option value="__agency__">Agency staff — type name below ↓</option>
        </optgroup>
      </select>
      <input type="text" id="tranesc-staff-custom" placeholder="Agency or other staff name" style="display:none;margin-top:6px;font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%;box-sizing:border-box">
    </div>
    <div class="row2">
      <div class="field"><label>Start time</label><input type="time" id="tranesc-start"></div>
      <div class="field"><label>End time</label><input type="text" id="tranesc-end" placeholder="e.g. 22:00 or 22:00+1"></div>
    </div>
    <div class="field"><label>Day of week</label>
      <select id="tranesc-day" style="font-size:12px;padding:6px;border-radius:var(--r);border:1px solid var(--bd2);width:100%">
        <option value="0">Monday</option><option value="1">Tuesday</option><option value="2">Wednesday</option>
        <option value="3">Thursday</option><option value="4">Friday</option><option value="5">Saturday</option><option value="6">Sunday</option>
      </select>
    </div>
    <div class="field"><label>Notes</label><input type="text" id="tranesc-note" placeholder="e.g. Local clinic — 2 youth"></div>
    <div style="display:flex;gap:8px;margin-top:.5rem">
      <button class="btn pri" style="flex:1" onclick="saveTranEsc()">Save</button>
      <button class="btn" style="flex:1;color:#c0392b;border-color:#f5c6cb" id="tranesc-delete-btn" onclick="deleteTranEsc()" style="display:none">Delete entry</button>
    </div>
  </div>
</div>

<div id="new-deadline-modal" class="modal-wrap">
  <div class="modal">
    <div class="modal-title">Add deadline / reminder <span class="mx" onclick="closeModal('new-deadline-modal')">×</span></div>
    <div class="field"><label>Title</label><input type="text" id="dl-title" placeholder="e.g. PP 08 Availability deadline"></div>
    <div class="row2">
      <div class="field"><label>Date</label><input type="date" id="dl-date"></div>
      <div class="field"><label>Time (optional)</label><input type="time" id="dl-time"></div>
    </div>
    <div class="field"><label>Visible to</label><select id="dl-vis"><option>All staff</option><option>Management only</option><option>Scheduling Admin only</option></select></div>
    <div class="field"><label>Details (optional)</label><textarea id="dl-notes" rows="2" placeholder="Any extra context..."></textarea></div>
    <button class="btn pri" style="width:100%" onclick="saveDeadline()">Add reminder</button>
  </div>
</div>

<div id="notif-wrap" style="position:fixed;top:56px;right:14px;z-index:300;width:270px"></div>

<script>
/* ===================== STATE ===================== */
let loginRole='mgmt', selLeaveVal='', dragIdx=null, senUnit='educators';
const WEEKS=[
  {label:'PP 07 — WEEK 1 (Jun 14–20)',cls:'',days:['S14','M15','T16','W17','T18','F19','S20']},
  {label:'PP 07 — WEEK 2 (Jun 21–27)',cls:'',days:['S21','M22','T23','W24','T25','F26','S27']},
  {label:'PP 08 — WEEK 3 (Jun 28–Jul 4)',cls:'pp2',days:['S28','M29','T30','W1','T2','F3','S4']},
  {label:'PP 08 — WEEK 4 (Jul 5–11)',cls:'pp2',days:['S5','M6','T7','W8','T9','F10','S11']},
];
const boData=[
  {emp:'Kerwin Guy-Roach',dates:'Jul 8',type:'Family',status:'pending'},
  {emp:'Tharani Siwalingam',dates:'Jun 23, Jun 26',type:'Vacation',status:'pending'},
  {emp:'Shannon Ridley',dates:'Jun 17, Jul 3, Jul 9',type:'Vacation',status:'pending'},
  {emp:'Eddy Bathalien',dates:'Jun 14, Jun 19',type:'Stat',status:'approved'},
  {emp:'Paul Vincent',dates:'Jul 4, Jul 5',type:'Vacation',status:'pending'},
];
const memoData=[
  {type:'escort',staff:"Mark D'Agostino",date:'Jun 16, 2026',youth:2,dest:'Kuujjuaq',start:'06:00',end:'18:00',notes:'Medical appointment escort. Return flight booked for same day.'},
  {type:'transport',staff:'Greg Page',date:'Jun 17, 2026',youth:1,dest:'Local — clinic',start:'12:00',end:'15:00',notes:'Agency staff (Ahmad*) to arrive 1hr before appointment.'},
  {type:'escort',staff:'Keith Burnett',date:'Jun 25, 2026',youth:3,dest:'Montreal',start:'05:30',end:'22:00',notes:'Court appearance escort. Overnight stay required, hotel booked.'},
];
const senData={
  educators:[
    {name:'Gilles Lezi',title:'Senior Educator',status:'FT',years:'15.56 yrs'},
    {name:'Eddy Bathalien',title:'Senior Educator',status:'FT',years:'15.34 yrs'},
    {name:'Makeda Samuels',title:'Educator',status:'FT',years:'15.26 yrs'},
    {name:'Michael Flemming',title:'Educator',status:'FT',years:'14.95 yrs'},
    {name:'Kerwin Guy-Roach',title:'Educator',status:'TFT',years:'11.46 yrs'},
    {name:'Ansonia Arrington',title:'Educator',status:'TFT',years:'10.19 yrs'},
    {name:'Yvonne Kaberamanzi',title:'Educator',status:'PT',years:'9.37 yrs'},
    {name:'Shannon Ridley',title:'Educator',status:'PT',years:'8.12 yrs'},
  ],
  ia:[
    {name:'Jean Nicolas Michaud',title:'Senior Intervention Agent',status:'FT',years:'15.52 yrs'},
    {name:'Keith Burnett',title:'Senior Intervention Agent',status:'FT',years:'15.20 yrs'},
    {name:"Mark D'Agostino",title:'Intervention Agent',status:'FT',years:'14.88 yrs'},
    {name:'Angelo Kontakos',title:'Intervention Agent',status:'FT',years:'13.45 yrs'},
    {name:'Greg Page',title:'Intervention Agent',status:'FT',years:'12.30 yrs'},
    {name:'Steven Yearwood',title:'Intervention Agent',status:'PT',years:'9.10 yrs'},
    {name:'Keon Pompey',title:'Intervention Agent',status:'PT',years:'7.88 yrs'},
    {name:'Braydon Burnett',title:'Intervention Agent',status:'TFT',years:'5.22 yrs'},
  ]
};
const schedStaff=[
  {name:'Keith Burnett',meta:'FT',mine:true,
   cells:['J/S','','','','J/S','','','','J/S','ESC','R','','','','','','','','J/S sw','','','','S/T','','','','J/S','',''],
   cover:['','','','','','','','','','Tracy A.*','','','','','','','','','','','','','','','','','','']},
  {name:"Mark D'Agostino",meta:'FT',mine:false,
   cells:['S','','S','TRAN','S','sw','S','','','','R','','','','','','J','','J','','J sw','J/T','','','','J','',''],
   cover:['','','','Greg P.','','','','','','','','','','','','','','','','','','','','','','','','']},
  {name:'Greg Page',meta:'FT',mine:false,cells:['','OT','S','','J','','J/S','','','','J','','','','','','J/S sw','','','','','','J/T','','J/S','','',''],cover:[]},
  {name:'J-N Michaud',meta:'FT',mine:false,cells:['J','','','','J','','J','','J','','J','','','','','','S','','S','','','','S/T','','S','','S',''],cover:[]},
  {name:'Angelo Kontakos',meta:'FT',mine:false,cells:['','','J','','S','','S','','','','R','','S sw','S','','','','','J','','J sw','S/T','','S','','','',''],cover:[]},
  {name:'Steven Yearwood',meta:'PT',mine:false,cells:['S','','S','','J','','','','S sw','S','','','','','','','J','','','','J','','J/T','','J','','J',''],cover:[]},
  {name:'Keon Pompey (J)',meta:'PT',mine:false,cells:['','','J','','','','','','','','S','','S','','S','','','','','','S','','','','','','',''],cover:[]},
  {name:'Errol A. Green',meta:'PT',mine:false,cells:['','','','','N','','','','','','N','','N','','N','','N','','','','','','N','','N','','',''],cover:[]},
];

/* ===================== NAV ===================== */
function setRole(r,el){
  loginRole=r;
  document.querySelectorAll('.role-opt').forEach(x=>x.classList.remove('on'));
  el.classList.add('on');
}
function doLogin(){
  document.getElementById('p-login').classList.remove('on');
  if(loginRole==='mgmt'){
    document.getElementById('mgmt-nav').style.display='flex';
    document.getElementById('emp-nav').style.display='none';
    page('overview',document.querySelector('#mgmt-nav .nav-item'));
  } else {
    document.getElementById('emp-nav').style.display='flex';
    document.getElementById('mgmt-nav').style.display='none';
    buildEmpSchedule();
    buildEmpMsg();
    buildEmpSeniority();
    empPage('emp-schedule',document.querySelector('#emp-nav .nav-item'));
  }
}
function logout(){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.getElementById('p-login').classList.add('on');
  document.getElementById('mgmt-nav').style.display='none';
  document.getElementById('emp-nav').style.display='none';
}
function page(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.getElementById('p-'+id).classList.add('on');
  document.querySelectorAll('#mgmt-nav .nav-item').forEach(n=>n.classList.remove('on'));
  if(el) el.classList.add('on');
  if(id==='bookoffs') renderBOTable();
  if(id==='memos') renderMemos();
  if(id==='seniority') renderSen();
  if(id==='messaging') buildMsgArea();
  if(id==='availability') renderAvailMgmt();
  if(id==='deadlines') renderDeadlines();
  if(id==='negtimes') renderNegTimeMgmt();
  if(id==='oncall'){oncallTab('pkg',document.getElementById('oncall-tab-pkg'));}
  if(id==='roster') renderRoster();
  if(id==='weeklysummary') renderSchedPushLog();
  if(id==='availability') renderAvailPT();
}
function empPage(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.getElementById('p-'+id).classList.add('on');
  document.querySelectorAll('#emp-nav .nav-item').forEach(n=>n.classList.remove('on'));
  if(el) el.classList.add('on');
  if(id==='emp-unfilled') renderUnfilledShifts();
  if(id==='emp-seniority') buildEmpSeniority();
}

/* ===================== SCHEDULE GRID ===================== */
function cellClass(v){
  if(!v||v==='—') return 'em';
  const u=v.toUpperCase().replace(/\s*(SW|\/T)\s*/g,'').trim();
  // OT subtypes (OT·J1, OT·S1, OT·N, etc.) — must come before J/S checks
  if(u.startsWith('OT')) return 'OT';
  if(u==='TRAN') return 'TRAN';
  if(u==='ESC') return 'ESC';
  if(u==='R') return 'R';
  if(u==='N') return 'N';
  if(u==='J2') return 'J2';
  if(u==='S2') return 'S2';
  // Double shifts J/S — treat as J1 colour
  if(u.includes('J/S')||u.includes('J1/S')||u.includes('J2/S')) return 'J1';
  if(u==='J1/T'||u==='J/T'||u[0]==='J') return 'J1';
  if(u==='S1/T'||u==='S/T'||u[0]==='S') return 'S1';
  if(u.includes('VAC')||u.includes('V')) return 'V';
  return 'em';
}
/* ---- per-cell overrides (set by saveCellEdit) ---- */
const cellOverrides={};  // key = "si-idx": {start,end,name,bookoff,shift}

/* ---- custom legend entries (management can add/remove) ---- */
const customLegendEntries=[];  // [{code, label}]
function openLegendAdd(containerId){
  const code=prompt('Shift code (e.g. J4, OT·S3, J1/T):','');
  if(!code) return;
  const label=prompt('Description (e.g. Day 4, OT Evening 3):','');
  if(label===null) return;
  customLegendEntries.push({code:code.trim(),label:label.trim()});
  buildGrid(containerId, true, currentGridStaff);
}
function removeLegendEntry(idx,containerId){
  customLegendEntries.splice(idx,1);
  buildGrid(containerId, true, currentGridStaff);
}

const tranEscRows=[
  {pp:0,day:1,type:'TRAN',staff:'Mark D\'Agostino',start:'12:00',end:'15:00',note:'Local clinic — 2 youth'},
  {pp:1,day:3,type:'ESC',staff:'Keith Burnett',start:'05:30',end:'22:00+1',note:'Northern escort — Montreal court, 3 youth. Overnight.'},
];

const schedStaffEd=[
  {name:'Gilles Lezi',meta:'FT Ed',mine:false,
   cells:['J1','','J1','','J1','','J1','','J1','J1','','','','','','','J2','','J2','','','','J1/T','','J1','','J1',''],
   cover:['','','','','','','','','','Ansonia','','','','','','','','','','','','','','','','','',''],
   bookoff:['','','','','','','','','','VAC','','','','','','','','','','','','','','','','','','']},
  {name:'Eddy Bathalien',meta:'FT Ed',mine:false,
   cells:['S1','','','','S1','','S2','','','','S1','','S1','','','','S2 sw','','S1','','S1 sw','S1/T','','','','S1','',''],
   cover:['','','','','','','','','','','','','','','','','Makeda','','','','Kerwin','','','','','','',''],
   bookoff:[]},
  {name:'Makeda Samuels',meta:'FT Ed',mine:false,
   cells:['','','J2','','S1','','S1','','','','J2','','J2','','J2','','','','J1','','J1 sw','J1/T','','J1','','','',''],
   cover:['','','','','','','','','','','','','','','','','','','','','Ansonia','','','','','','',''],
   bookoff:[]},
  {name:'Kerwin Guy-Roach',meta:'TFT Ed',mine:false,
   cells:['N','','N','','','','N','','N','','','','N','','N','','N','','','','N','','N/T','','N','','',''],
   cover:[],bookoff:[]},
  {name:'Ansonia Arrington',meta:'TFT Ed',mine:false,
   cells:['','OT·S2','S2','','J2','','J2','','','','J2','','','','J2','','J2 sw','','J2','','J2 sw','J2/T','','J2','','J2','',''],
   cover:['','','','','','','','','','','','','','','','','Eddy','','','','Eddy','','','','','','',''],
   bookoff:[]},
  {name:'Yvonne Kaberamanzi',meta:'PT Ed',mine:false,
   cells:['','','S2','','','','','','S2','S2','','','','','','','J1','','','','J1','','','','','','J1',''],
   cover:[],bookoff:[]},
  {name:'Shannon Ridley',meta:'PT Ed',mine:false,
   cells:['','','','','J2','','J2','','','','','','J1','','S1','','','','','','S1','','','','','','',''],
   cover:[],bookoff:[]},
];
const schedStaffIA=[
  {name:'Keith Burnett',meta:'FT IA',mine:true,
   cells:['J1','','','','J1','','J1','','J1','J1','R','','','','','','','','J1 sw','','','','S1/T','','','','J1',''],
   cover:['','','','','','','','','','Tracy*','','','','','','','','','Angelo','','','','','','','','',''],
   bookoff:['','','','','','','','','','VAC','','','','','','','','','','','','','','','','','','']},
  {name:"Mark D'Agostino",meta:'FT IA',mine:false,
   cells:['S1','','S1','S1','S1','','S1','','','','R','','','','','','J1','','J1','','J1 sw','J1/T','','','','J1','',''],
   cover:['','','','Angelo','','','','','','','','','','','','','','','','','Greg','','','','','','',''],
   bookoff:['','','','VAC','','','','','','','','','','','','','','','','','','','','','','','','']},
  {name:'Greg Page',meta:'FT IA',mine:false,
   cells:['','OT·J1','S1','','J1','','J1','','','','J1','','','','','','J1 sw','','','','','','J1/T','','J1','','',''],
   cover:['','','','','','','','','','','','','','','','','Mark','','','','','','','','','','',''],
   bookoff:[]},
  {name:'Jean-N. Michaud',meta:'FT IA',mine:false,
   cells:['J1','','','','J1','','J1','','J1','','J1','','','','','','S1','','S1','','','','S1/T','','S1','','S1',''],
   cover:[],bookoff:[]},
  {name:'Angelo Kontakos',meta:'FT IA',mine:false,
   cells:['','','J1','','S1','','S1','','','','R','','S1 sw','S1','','','','','J1','','J1 sw','J1/T','','S1','','','',''],
   cover:['','','','','','','','','','','','','Keith','','','','','','','','Keith','','','','','','',''],
   bookoff:[]},
  {name:'Tracy Adam',meta:'FT IA',mine:false,
   cells:['J1','','J1','','J1','','','','J1','OT·J1','','','J1','','J1','','','','S1','','S1','S1/T','','','','S1','',''],
   cover:[],bookoff:[]},
  {name:'Jema Rattray',meta:'FT IA',mine:false,
   cells:['S1','','','','S1 sw','S1','S1','','S1','','','','S1','','S1','','J1','','J1','','','','J1/T','','J1','','',''],
   cover:['','','','','Steven','','','','','','','','','','','','','','','','','','','','','','',''],
   bookoff:[]},
  {name:'Mahkeda Newton',meta:'TFT IA',mine:false,
   cells:['','','J1 sw','J1','','','J1','','','','J1','','','','J1','','','','J1','','J1','J1/T','','','','J1','',''],
   cover:['','','Greg','','','','','','','','','','','','','','','','','','','','','','','','',''],
   bookoff:[]},
  {name:'Steven Yearwood',meta:'PT IA',mine:false,
   cells:['S1','','S1','','J1','','','','S1 sw','S1','','','','','','','J1','','','','J1','','J1/T','','J1','','J1',''],
   cover:['','','','','','','','','Jema','','','','','','','','','','','','','','','','','','',''],
   bookoff:[]},
  {name:'Keon Pompey',meta:'PT IA',mine:false,
   cells:['','','J1','','','','','','','','S1','','S1','','S1','','','','','','S1','','','','','','',''],
   cover:[],
   bookoff:['','','','','','','','','','','SICK','','','','','','','','','','','','','','','','','']},
  {name:'Errol A. Green',meta:'PT IA',mine:false,
   cells:['','','','','N','','','','','','N','','N','','N','','N','','','','','','N','','N','','',''],
   cover:[],bookoff:[]},
  {name:'Darlene Okafor',meta:'PT IA',mine:false,
   cells:['','J1','','','','J1','','J1','','','','J1','','','','J1','','J1','','','','J1','','J1','','','',''],
   cover:[],bookoff:[]},
];

function buildGrid(containerId, isMgmt, staffList){
  const staff=staffList||schedStaffIA;
  let h='';
  WEEKS.forEach((wk,wi)=>{
    h+='<div class="wk-label '+wk.cls+'">'+wk.label+'</div>';
    h+='<table class="sg"><thead><tr><th class="nh">Staff</th>';
    wk.days.forEach(d=>h+='<th>'+d+'</th>');
    // +Cell extra column removed
    h+='</tr></thead><tbody>';
    staff.forEach((s,si)=>{
      const metaParts=s.meta.split(' ');
      const empType=metaParts[0]; // FT, PT, TFT, Recall
      const roleLabel=metaParts.slice(1).join(' '); // IA, Ed, etc.
      const metaDisplay=roleLabel?empType+' &bull; '+roleLabel:empType;
      h+='<tr class="'+(s.mine?'mine':'')+'"><td class="nh"><span class="td nm">'+s.name+'</span><span class="mt">'+metaDisplay+'</span></td>';
      for(let i=0;i<7;i++){
        const idx=wi*7+i;
        const oKey=si+'-'+idx;
        const ov=cellOverrides[oKey]||{};
        const rawCode=s.cells&&s.cells[idx]?s.cells[idx]:'';
        // shift type: override from modal (ov.shift) overrides raw cell code
        const shiftRaw=ov.shift||rawCode;
        // parse base shift and SW/Training suffix
        const baseCode=shiftRaw.replace(/\s*(sw|\/T)\s*/gi,'').trim();
        const isSw=/ sw/i.test(shiftRaw);
        const isTraining=/\/T/i.test(shiftRaw);
        // book-off code (leave): stored in ov.bookoff OR s.bookoff array
        const bookoff=ov.bookoff||(s.bookoff&&s.bookoff[idx]?s.bookoff[idx]:'');
        // cover/replacement name from override or data array
        const cover=ov.name||(s.cover&&s.cover[idx]?s.cover[idx]:'');
        const cc=cellClass(baseCode);
        const customTime=(ov.start&&ov.end)?ov.start+'–'+ov.end:'';
        const isEmpty=!baseCode&&!bookoff;
        const label=s.name+' · '+wk.days[i];
        let cellClick='';
        if(isMgmt){
          cellClick="onclick=\"openCellEdit(this,'"+label+"')\" style=\"cursor:pointer\"";
        }
        // Build cell interior
        const isAgency=cover&&cover.includes('*');
        // TOP ROW: shift code + SW + /T + bookoff code — ALL inline on same line
        let topLine='<div style="display:flex;align-items:center;gap:2px;flex-wrap:wrap;justify-content:center;line-height:1.2">'
          +'<span class="cell-main">'+(baseCode||'—')+'</span>';
        if(isSw) topLine+='<span style="background:#D7E8FF;color:#1a3a6e;border-radius:2px;font-size:7px;font-weight:800;padding:0 3px">SW</span>';
        if(isTraining) topLine+='<span style="background:#E0F2F1;color:#00695C;border-radius:2px;font-size:7px;font-weight:800;padding:0 3px">/T</span>';
        // book-off code INLINE right next to shift code — same row
        if(bookoff) topLine+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:7px;font-weight:800;padding:0 3px;letter-spacing:.3px">'+bookoff+'</span>';
        topLine+='</div>';
        let interior=topLine;
        // SECOND ROW: cover/replacement name OR SW partner name — below the codes
        if(cover){
          const nameDisplay=cover.replace('*','');
          const agencyStar=isAgency?'<span style="color:#f59e0b;font-weight:900">*</span>':'';
          const arrow=isSw?'⇄':'▶';
          interior+='<span style="color:#fff;background:rgba(0,0,0,.28);border-radius:2px;font-size:8px;font-weight:700;padding:1px 3px;display:block;margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:70px">'+arrow+' '+nameDisplay+agencyStar+'</span>';
        }
        // THIRD ROW: custom time if set
        if(customTime) interior+='<span style="font-size:8px;color:rgba(255,255,255,.8);font-weight:600;display:block;margin-top:1px">⏱ '+customTime+'</span>';
        // empty cell in mgmt: clickable with faint + hint
        if(isEmpty&&!isMgmt){
          h+='<td class="std"><div class="cell em">—</div></td>';
        } else {
          const emptyHint=isEmpty?'<span style="font-size:14px;color:rgba(0,0,0,.18);line-height:1">+</span>':'';
          h+='<td class="std"><div class="cell '+(isEmpty?'em':cc)+'" '+cellClick+' data-si="'+si+'" data-idx="'+idx+'">'+interior+(isEmpty?emptyHint:'')+'</div></td>';
        }
      }
      // NO extra +Cell column — removed per request
      h+='</tr>';
    });

    // TRAN/ESC rows at bottom of each pay period week — always shown in mgmt, shown only if entries exist in employee view
    const tranRows=tranEscRows.filter(r=>r.pp===wi);
    if(tranRows.length||isMgmt){
      h+='<tr><td class="nh" style="background:var(--bg2)">'
        +'<span class="td nm" style="color:var(--t3);font-size:9px">TRAN / ESC</span>'
        +(isMgmt?'<span class="mt"><button style="font-size:8px;padding:1px 4px;border:1px solid var(--bd2);border-radius:3px;background:var(--bg1);cursor:pointer;margin-top:2px" onclick="openAddTranEsc('+wi+')">+ Add</button></span>':'')
        +'</td>';
      const dayMap={};
      tranRows.forEach(r=>dayMap[r.day]=r);
      for(let i=0;i<7;i++){
        const r=dayMap[i];
        if(r){
          const cc=r.type==='TRAN'?'TRAN':'ESC';
          const editAttr=isMgmt?' onclick="openEditTranEsc('+tranEscRows.indexOf(r)+')" style="cursor:pointer"':'onclick="openTranDetail(\''+r.type+'\',\''+r.staff+'\')" style="cursor:pointer"';
          h+='<td class="std"><div class="cell '+cc+'" '+editAttr+' style="font-size:9px;line-height:1.3">'
            +'<span style="font-weight:800">'+r.type+'</span>'
            +'<span style="display:block;font-size:8px;margin-top:1px">'+r.staff+'</span>'
            +'<span style="display:block;font-size:8px;color:rgba(255,255,255,.7)">'+r.start+'–'+r.end+'</span>'
            +'</div></td>';
        } else {
          if(isMgmt){
            h+='<td class="std"><div class="cell em" style="cursor:pointer;font-size:12px;color:var(--t3)" onclick="openAddTranEscDay('+wi+','+i+')">+</div></td>';
          } else {
            h+='<td class="std"><div class="cell em" style="font-size:10px;color:var(--t3)">—</div></td>';
          }
        }
      }
      if(isMgmt) h+='<td></td>';
      h+='</tr>';
    }

    h+='</tbody></table>';
  });
  // Shift type legend
  h+='<div class="legend" id="shift-legend-'+containerId+'">';
  h+='<div class="lgi"><div class="lgd J1">J1/J2/J3</div>Day</div>';
  h+='<div class="lgi"><div class="lgd S1">S1/S2/S3</div>Evening</div>';
  h+='<div class="lgi"><div class="lgd N">N</div>Night</div>';
  h+='<div class="lgi"><div class="lgd OT">OT·J/OT·S</div>Overtime</div>';
  h+='<div class="lgi"><div class="lgd J1">J/S</div>Double shift</div>';
  h+='<div class="lgi"><div class="lgd TRAN">TRAN</div>Transport</div>';
  h+='<div class="lgi"><div class="lgd ESC">ESC</div>Escort</div>';
  // Render custom legend entries
  customLegendEntries.forEach((e,ei)=>{
    h+='<div class="lgi" style="position:relative">'
      +'<div class="lgd" style="background:#6c757d;color:#fff">'+e.code+'</div>'+e.label
      +(isMgmt?'<span style="margin-left:4px;cursor:pointer;color:var(--t3);font-size:10px" onclick="removeLegendEntry('+ei+',\''+containerId+'\')">✕</span>':'')
      +'</div>';
  });
  if(isMgmt){
    h+='<div class="lgi"><button onclick="openLegendAdd(\''+containerId+'\')" style="font-size:9px;padding:2px 7px;border:1px dashed var(--bd2);border-radius:3px;background:transparent;cursor:pointer;color:var(--t3)">+ Add code</button></div>';
  }
  h+='</div>';
  // Leave / book-off codes row
  h+='<div style="font-size:10px;color:var(--t3);padding:.4rem 0 .1rem;border-top:1px solid var(--bd);margin-top:.2rem;display:flex;flex-wrap:wrap;gap:6px;align-items:center">';
  h+='<span style="font-weight:700;color:var(--t2)">Leave codes:</span>';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">VAC</span> Vacation &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">SICK</span> Sick leave &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">STAT</span> Statutory holiday &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">PSYCH</span> Psychological day &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">PEXT</span> Bank time &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">OT-TAKEN</span> OT taken &nbsp;';
  h+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:9px;font-weight:800;padding:1px 4px">CNESST</span> Work injury';
  h+='</div>';
  // Symbol key
  h+='<div style="font-size:10px;color:var(--t3);padding:.25rem 0 .1rem;display:flex;flex-wrap:wrap;gap:10px;align-items:center">';
  h+='<span><span style="color:#f59e0b;font-weight:900;font-size:12px">*</span> Agency staff</span>';
  h+='<span><span style="background:rgba(0,0,0,.18);color:#fff;border-radius:2px;font-size:9px;font-weight:700;padding:1px 4px">⇄ Name</span> shift switch partner</span>';
  h+='<span><span style="background:rgba(0,0,0,.18);color:#fff;border-radius:2px;font-size:9px;font-weight:700;padding:1px 4px">▶ Name</span> replacement / coverage</span>';
  h+='<span>/T = in training</span>';
  h+='</div>';
  if(isMgmt) h+='<div class="info" style="margin-top:.5rem;font-size:11px">💡 Click any cell to edit shift type, times, coverage name, or apply a leave code. Use the <b>+ Add code</b> button to add a custom shift type to the legend.</div>';
  document.getElementById(containerId).innerHTML=h;
}

/* blank cell add for management */
function addBlankCell(wi,si,btn){
  const staffList=currentGridStaff||schedStaffIA;
  const s=staffList[si];
  const label=s.name+' · Week '+(wi+1)+' — New cell';
  // find the td of the + button and use it as context
  openCellEdit(btn.closest('div'),label);
}

let currentGridStaff=null;
function showFullGrid(name, staffList){
  currentGridStaff=staffList||null;
  const el=document.getElementById('full-grid-area');
  // build unit tab selector
  el.innerHTML='<div class="card">'
    +'<div style="display:flex;gap:6px;align-items:center;margin-bottom:.8rem;flex-wrap:wrap">'
    +'<div class="card-title" style="margin:0">'+name+' — full grid</div>'
    +'<button class="btn pri sm" onclick="openModal(\'cell-edit-modal\')" style="font-size:11px">+ Add/edit cell</button>'
    +'</div>'
    +'<div class="sched-scroll" id="mgmt-full-grid"></div></div>';
  buildGrid('mgmt-full-grid',true,staffList||schedStaffIA);
  el.scrollIntoView({behavior:'smooth'});
}
function buildEmpSchedule(){
  const el=document.getElementById('sp-boys-ia');
  el.innerHTML='<div class="home-banner">📌 This is your home screen — Boys IA, your pinned schedule.</div><div class="sched-scroll" id="emp-grid"></div>';
  buildGrid('emp-grid',false,schedStaffIA);
}
function empSchedTab(id,el){
  document.querySelectorAll('.sched-panel').forEach(p=>p.classList.remove('on'));
  document.getElementById('sp-'+id).classList.add('on');
  document.querySelectorAll('.st').forEach(t=>t.classList.remove('on'));
  el.classList.add('on');
}
function setEmpHome(pin){
  document.querySelectorAll('.pin').forEach(p=>{p.classList.remove('hp');p.textContent='📍';});
  pin.classList.add('hp');pin.textContent='📌';
}

/* ===================== TRAN/ESC DETAIL ===================== */
const tranDetails={
  "ESC-Keith Burnett":{title:'Northern escort — Keith Burnett',data:{'Number of youth':'3','Destination':'Montreal','Start time':'05:30','End time':'22:00 (next day)','Covering staff':'Tracy Adam* (agency)','Notes':'Court appearance escort. Overnight stay, hotel booked.'}},
  "TRAN-Mark D'Agostino":{title:"Transportation — Mark D'Agostino",data:{'Number of youth':'2','Destination':'Local clinic appointment','Start time':'12:00','End time':'15:00','Covering staff':'Greg Page (shift swapped to cover)'}},
};
function openTranDetail(code,name){
  const key=code+'-'+name;
  const d=tranDetails[key]||{title:code+' detail — '+name,data:{Info:'Contact management for full details.'}};
  document.getElementById('tran-title').textContent=d.title;
  document.getElementById('tran-body').innerHTML=Object.entries(d.data).map(([k,v])=>'<div class="memo-field"><div class="memo-label">'+k+'</div><div class="memo-val">'+v+'</div></div>').join('');
  openModal('tran-modal');
}

/* ===================== OT ===================== */
function otAction(name,action){
  const r=document.getElementById('ot-result');
  const t=document.getElementById('ot-contact-time');
  const contactTime=t&&t.value?t.value:new Date().toLocaleString('en-CA',{month:'short',day:'numeric',hour:'2-digit',minute:'2-digit'});
  if(action==='T'){
    r.innerHTML='<div class="info" style="border-left:3px solid var(--green)">✓ <b>'+name+'</b> accepted the OT shift. Contacted: '+contactTime+'. Email confirmation sent to employee + management. Name added to schedule as cover.</div>';
  } else if(action==='R'){
    r.innerHTML='<div class="info" style="border-left:3px solid var(--amber)">📋 <b>'+name+'</b> refused. Contacted: '+contactTime+'. Email with timestamp sent to employee + management. Logged in OT history. Advancing to next person.</div>';
  } else {
    r.innerHTML='<div class="info" style="border-left:3px solid var(--t3)">📵 <b>'+name+'</b> — no answer. Contacted: '+contactTime+'. Logged. Advancing to next person in rotation.</div>';
  }
  r.scrollIntoView({behavior:'smooth'});
}

/* ===================== BOOK-OFFS ===================== */
function renderBOTable(){
  const t=document.getElementById('bo-mgmt-table');
  t.innerHTML='<thead><tr><th>Employee</th><th>Date(s)</th><th>Type</th><th>Status</th><th>Action</th></tr></thead><tbody>'+
    boData.map((r,i)=>'<tr><td><b>'+r.emp+'</b></td><td>'+r.dates+'</td><td>'+r.type+'</td><td>'+(r.status==='approved'?'<span class="badge b-act">Approved</span>':'<span class="badge b-sus">Pending</span>')+'</td><td>'+(r.status==='approved'?'—':'<button class="btn sm grn" onclick="approveBO('+i+')">Approve</button> <button class="btn sm red" onclick="denyBO('+i+')">Deny</button>')+'</td></tr>').join('')+'</tbody>';
}
function approveBO(i){boData[i].status='approved';renderBOTable();notify(boData[i].emp+' book-off approved. Email sent to employee and manager.');}
function denyBO(i){const n=boData[i].emp;boData.splice(i,1);renderBOTable();notify(n+'\'s book-off denied. Employee notified by app + email.');}

/* ===================== EMPLOYEE BOOK-OFF ===================== */
function selLeave(el,v){document.querySelectorAll('.ltab').forEach(t=>t.classList.remove('on'));el.classList.add('on');selLeaveVal=v;document.getElementById('leave-err').style.display='none';}
function check24(v){if(!v)return;const diff=(new Date(v+'T00:00:00')-new Date())/(3600000);document.getElementById('u24-warn').style.display=diff<24?'block':'none';}
function submitBO(){
  if(!selLeaveVal){document.getElementById('leave-err').style.display='block';return;}
  const d=document.getElementById('bo-date').value;
  if(!d){alert('Please select a date.');return;}
  notify('Your '+selLeaveVal+' book-off for '+d+' has been submitted. Management will be notified by app + email.');
  selLeaveVal='';document.querySelectorAll('.ltab').forEach(t=>t.classList.remove('on'));
}

/* ===================== MESSAGING ===================== */
function buildMsgArea(){
  document.getElementById('msg-area').innerHTML=msgHTML('Wesley Thomas','WT');
  document.getElementById('emp-msg-area').innerHTML=msgHTML('Jema Rattray','JR');
  document.getElementById('emp-msg-full').innerHTML=msgHTML('Mahkeda Newton','MN');
}
function buildEmpMsg(){buildMsgArea();}
function msgHTML(name,initials){
  return '<div class="msg-app"><div class="msg-sb"><div class="msg-sb-head">Messages</div>'+
    '<div class="conv on"><div class="av">'+initials+'</div><div><div class="cv-name">'+name+'</div><div class="cv-prev">Switch proposal</div></div></div>'+
    '<div class="conv"><div class="av" style="background:#ADD8E6;color:#0C447C">MP</div><div><div class="cv-name">Matthew Pike</div><div class="cv-prev">Can you cover Sat?</div></div></div>'+
    '</div><div class="msg-main"><div class="msg-head">'+name+'</div><div class="msg-body">'+
    '<div class="bub them">Hey — can you switch your evening Jun 23 for my day Jun 24?</div>'+
    '<div class="bub me">Yeah that works, sending the formal request</div>'+
    '<div class="sw-card"><div class="sw-title">↔ Switch proposal</div>'+
    '<div class="sw-row"><span>You give</span><b>Tue Jun 23 — Evening (S/T)</b></div>'+
    '<div class="sw-row"><span>You receive</span><b>Wed Jun 24 — Day (J1)</b></div>'+
    '<div class="sw-row"><span>Unit</span><b>Girls Educators (same unit)</b></div>'+
    '<div class="sw-status"><span class="pill done">✓ You agreed</span><span class="pill wait">⏳ '+name+' — pending</span><span class="pill pend">🛡 Management — pending</span></div>'+
    '<div style="font-size:9px;color:var(--blue);margin-top:6px">✉ Email + app notification sent to '+name+'</div>'+
    '<div class="sw-status" style="margin-top:.4rem"><button class="btn sm grn" onclick="notify(\''+name+' agreed! Request now in management approval queue. Email + app notification sent to both parties.\')">Agree to switch</button> <button class="btn sm red" onclick="notify(\'Declined. The requesting employee has been notified. Request closed.\')">Decline</button></div>'+
    '</div></div>'+
    '<div class="msg-input"><button class="sw-trigger" onclick="alert(\'Opens structured switch proposal form.\')">↔ Propose switch</button><input type="text" placeholder="Type a message..."><button class="btn pri" onclick="notify(\'Message sent.\')">Send</button></div>'+
    '</div></div>';
}

/* ===================== MEMOS ===================== */
function renderMemos(){
  document.getElementById('memo-list').innerHTML=memoData.map((m,i)=>`
    <div class="memo-card">
      <span class="memo-type ${m.type==='escort'?'mt-escort':'mt-transport'}">${m.type==='escort'?'✈️ Northern escort':'🚌 Transportation shift'}</span>
      <div class="memo-title">${m.staff} — ${m.date}</div>
      <div class="memo-grid">
        <div class="memo-field"><div class="memo-label">Number of youth</div><div class="memo-val">${m.youth}</div></div>
        <div class="memo-field"><div class="memo-label">Destination / community</div><div class="memo-val">${m.dest}</div></div>
        <div class="memo-field"><div class="memo-label">Start time</div><div class="memo-val">${m.start}</div></div>
        <div class="memo-field"><div class="memo-label">End time</div><div class="memo-val">${m.end}</div></div>
      </div>
      <div style="font-size:12px;color:var(--t2)">${m.notes}</div>
    </div>`).join('');
}
function saveMemo(){
  const m={type:document.getElementById('m-type').value,staff:document.getElementById('m-staff').value||'—',date:document.getElementById('m-date').value||'—',youth:document.getElementById('m-youth').value||0,dest:document.getElementById('m-dest').value||'—',start:document.getElementById('m-start').value||'—',end:document.getElementById('m-end').value||'—',notes:document.getElementById('m-notes').value};
  memoData.unshift(m);closeModal('new-memo-modal');renderMemos();notify('Memo saved for '+m.staff+'.');
}

/* ===================== EMPLOYEE SENIORITY (read-only) ===================== */
function empSenUnit(unit, btn){
  document.getElementById('sen-emp-ed-btn').style.background='';
  document.getElementById('sen-emp-ed-btn').style.color='';
  document.getElementById('sen-emp-ed-btn').style.borderColor='';
  document.getElementById('sen-emp-ia-btn').style.background='';
  document.getElementById('sen-emp-ia-btn').style.color='';
  document.getElementById('sen-emp-ia-btn').style.borderColor='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  const label=unit==='educators'?'Educators':'Intervention Agents';
  document.getElementById('emp-sen-title').textContent=label+' — Seniority List';
  const list=senData[unit];
  document.getElementById('emp-sen-table').innerHTML='<thead><tr><th>#</th><th>Name</th><th>Status</th><th>Seniority</th></tr></thead><tbody>'+
    list.map((s,i)=>'<tr'+(s.name==='Keith Burnett'?' style="background:#FFFCE8"':'')+'><td><b>'+(i+1)+'</b></td><td>'+s.name+(s.name==='Keith Burnett'?' <span class="badge b-ft" style="font-size:9px">You</span>':'')+'</td><td>'+s.status+'</td><td>'+s.years+'</td></tr>').join('')+'</tbody>';
}
function buildEmpSeniority(){empSenUnit('ia',document.getElementById('sen-emp-ia-btn'));}

/* ===================== SENIORITY ===================== */
senUnit='ia'; // reset to default (declared above)
function renderSen(){renderSenNew();}
function moveSen(i,d){const l=senData[currentSenUnit];const j=i+d;if(j<0||j>=l.length)return;[l[i],l[j]]=[l[j],l[i]];renderSenNew();}
function dragStart(i){dragIdx=i;setTimeout(()=>document.querySelectorAll('.sen-row')[i].classList.add('dragging'),0);}
function dragDrop(e,i){e.preventDefault();if(dragIdx===null||dragIdx===i)return;const l=senData[currentSenUnit];const it=l.splice(dragIdx,1)[0];l.splice(i,0,it);dragIdx=null;renderSenNew();}
function dragEnd(){document.querySelectorAll('.sen-row').forEach(r=>r.classList.remove('dragging'));}

/* ===================== MODALS ===================== */
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}

/* ===================== MEMO TABS ===================== */
function memoTab(tab, btn){
  ['tran','gen','dm'].forEach(t=>{
    document.getElementById('memo-panel-'+t).style.display='none';
    document.getElementById('memo-tab-'+t).style.background='';
    document.getElementById('memo-tab-'+t).style.color='';
    document.getElementById('memo-tab-'+t).style.borderColor='';
  });
  document.getElementById('memo-panel-'+tab).style.display='block';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  if(tab==='tran') renderMemos();
  if(tab==='gen') renderGenMemos();
  if(tab==='dm') renderDMLog();
}

/* ===================== GENERAL MEMOS ===================== */
const genMemoData=[
  {subject:'PP 08 schedule now published',to:'All staff',from:'Scheduling Admin',date:'Mon Jun 16 at 8:05 AM',body:'The PP 08 schedule (Jun 28–Jul 11) is now live in the app. Please review your shifts and submit any concerns by Wednesday.',priority:'Normal'},
  {subject:'Availability deadline reminder — PP 09',to:'All staff',from:'Scheduling Admin',date:'Fri Jun 20 at 3:00 PM',body:'Reminder: PP 09 availability sheets are due by Wed Jun 25 at 9:00 AM. Late submissions will be placed at the bottom of the rotation.',priority:'Important'},
  {subject:'On-call change — this weekend',to:'All staff',from:'Unit Manager',date:'Fri Jun 20 at 4:45 PM',body:'Please note the on-call manager for this weekend (Jun 20–22) has changed. See the On-call tab for updated contact info.',priority:'Urgent'},
];
function renderGenMemos(){
  const el=document.getElementById('genmemo-list');if(!el)return;
  const prioColor={Normal:'var(--bluelight)',Important:'var(--amberlight)',Urgent:'var(--redlight)'};
  const prioText={Normal:'var(--blue)',Important:'var(--amber)',Urgent:'var(--red)'};
  el.innerHTML=genMemoData.map(m=>`
    <div class="card" style="border-left:3px solid ${prioText[m.priority]||'var(--bd)'}">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:6px">
        <div>
          <div style="font-weight:600;font-size:13px;margin-bottom:2px">${m.subject}</div>
          <div style="font-size:11px;color:var(--t2)">To: ${m.to} &nbsp;·&nbsp; From: ${m.from} &nbsp;·&nbsp; ${m.date}</div>
        </div>
        <span class="badge" style="background:${prioColor[m.priority]};color:${prioText[m.priority]}">${m.priority}</span>
      </div>
      <div style="font-size:12px;margin-top:8px;padding:8px;background:var(--bg1);border-radius:var(--r)">${m.body}</div>
    </div>`).join('');
}
function sendGenMemo(){
  const subj=document.getElementById('gm-subject').value||'General memo';
  const to=document.getElementById('gm-to').value;
  const body=document.getElementById('gm-body').value||'—';
  const prio=document.getElementById('gm-priority').value;
  genMemoData.unshift({subject:subj,to,from:'Scheduling Admin',date:new Date().toLocaleString('en-CA',{weekday:'short',month:'short',day:'numeric',hour:'2-digit',minute:'2-digit'}),body,priority:prio});
  closeModal('new-genmemo-modal');renderGenMemos();
  notify('Memo "'+subj+'" sent to '+to+'. In-app notification + email sent to all recipients.');
}

/* ===================== DIRECT MESSAGE ===================== */
const dmLog=[
  {to:'Keith Burnett',from:'Scheduling Admin',subject:'Coverage — Sat Jun 20',date:'Jun 18, 10:14 AM',preview:'Hi Keith, are you available to pick up the S1 shift on Jun 20?'},
  {to:'Gilles Lezi',from:'Unit Manager',subject:'OT offer — Jun 20 S1',date:'Jun 18, 10:30 AM',preview:'Gilles, you are next on the OT list for Jun 20. Please confirm by 12:00 PM.'},
];
function renderDMLog(){
  const el=document.getElementById('dm-log-table');if(!el)return;
  el.innerHTML='<thead><tr><th>To</th><th>From</th><th>Subject</th><th>Sent</th></tr></thead><tbody>'+
    dmLog.map(m=>'<tr><td>'+m.to+'</td><td>'+m.from+'</td><td>'+m.subject+'<div style="font-size:10px;color:var(--t3)">'+m.preview+'</div></td><td>'+m.date+'</td></tr>').join('')+'</tbody>';
}
function sendDM(){
  const to=document.getElementById('dm-to').value;
  const from=document.getElementById('dm-from').value;
  const subj=document.getElementById('dm-subject').value||'Message from management';
  const body=document.getElementById('dm-body').value||'—';
  dmLog.unshift({to,from,subject:subj,date:new Date().toLocaleString('en-CA',{month:'short',day:'numeric',hour:'2-digit',minute:'2-digit'}),preview:body.substring(0,60)+'…'});
  renderDMLog();
  notify('Direct message sent to '+to+'. In-app notification + email delivered.');
  document.getElementById('dm-subject').value='';document.getElementById('dm-body').value='';
}

/* ===================== UNFILLED SHIFTS / NEGOTIATED TIMES ===================== */
const unfilledShifts=[
  {date:'Sat Jun 20',shift:'S1 — 15:00–22:45',unit:'Boys IA',reason:'OT rotation exhausted',id:'unf1'},
  {date:'Fri Jun 20',shift:'N — 22:30–07:00',unit:'Girls IA',reason:'CNR — understaffed',id:'unf2'},
  {date:'Wed Jun 25',shift:'J1 — 07:00–14:45',unit:'Boys IA',reason:'Book-off (short notice)',id:'unf3'},
];
const negTimeRequests=[
  {emp:'Keith Burnett',date:'Sat Jun 20',shift:'S1 (15:00–22:45)',unit:'Boys IA',arrive:'17:00',leave:'22:45',notes:'Has a ride at 23:00',status:'pending'},
  {emp:'Steven Yearwood',date:'Fri Jun 20',shift:'N (22:30–07:00)',unit:'Girls IA',arrive:'22:30',leave:'03:00',notes:'Can only do first half of night',status:'pending'},
];
let currentUnfilledShift=null;
function renderUnfilledShifts(){
  const el=document.getElementById('unfilled-table');if(!el)return;
  el.innerHTML='<thead><tr><th>Date</th><th>Shift</th><th>Unit</th><th>Reason</th><th>Action</th></tr></thead><tbody>'+
    unfilledShifts.map(s=>'<tr style="background:#FFFCE8"><td><b>'+s.date+'</b></td><td>'+s.shift+'</td><td>'+s.unit+'</td><td>'+s.reason+'</td><td><button class="btn sm amb" onclick="openNegModal(\''+s.id+'\',\''+s.date+' — '+s.shift+'\')">Offer partial cover</button></td></tr>').join('')+'</tbody>';
}
function openNegModal(id,label){
  currentUnfilledShift=id;
  document.getElementById('negtime-shift-info').innerHTML='⚠️ Unfilled shift: <b>'+label+'</b>';
  openModal('negtime-modal');
}
function submitNegTime(){
  const arrive=document.getElementById('neg-arrive').value||'—';
  const leave=document.getElementById('neg-leave').value||'—';
  const notes=document.getElementById('neg-notes').value;
  closeModal('negtime-modal');
  notify('Partial cover submitted: arrive '+arrive+', leave by '+leave+'. Management will review and confirm. You will be notified by app + email.');
}
function renderNegTimeMgmt(){
  const el=document.getElementById('negtime-mgmt-table');if(!el)return;
  el.innerHTML='<thead><tr><th>Employee</th><th>Shift</th><th>Unit</th><th>Can arrive</th><th>Must leave by</th><th>Notes</th><th>Action</th></tr></thead><tbody>'+
    negTimeRequests.map((r,i)=>'<tr style="background:#FFFCE8"><td><b>'+r.emp+'</b></td><td>'+r.date+'<br><span style="font-size:10px;color:var(--t2)">'+r.shift+'</span></td><td>'+r.unit+'</td><td><b>'+r.arrive+'</b></td><td><b>'+r.leave+'</b></td><td style="font-size:11px;color:var(--t2)">'+r.notes+'</td><td><button class="btn sm grn" onclick="approveNeg('+i+')">Approve</button> <button class="btn sm red" onclick="denyNeg('+i+')">Deny</button></td></tr>').join('')+'</tbody>';
}
function approveNeg(i){const r=negTimeRequests[i];negTimeRequests.splice(i,1);renderNegTimeMgmt();notify(r.emp+' partial cover approved ('+r.arrive+'–'+r.leave+'). Name + adjusted times added to schedule. Employee notified.');}
function denyNeg(i){const r=negTimeRequests[i];negTimeRequests.splice(i,1);renderNegTimeMgmt();notify(r.emp+'\'s partial cover request denied. Employee notified by app + email.');}

/* ===================== AVAILABILITY ===================== */
const availData=[
  {name:'Kerwin Guy-Roach',type:'FT',submitted:'Jun 3, 8:47 AM',status:'on-time',compliant:true},
  {name:'Ansonia Arrington',type:'TFT',submitted:'Jun 3, 9:12 AM',status:'on-time',compliant:true},
  {name:'Steven Yearwood',type:'PT',submitted:'Jun 5, 11:30 AM',status:'on-time',compliant:true},
  {name:'Keon Pompey',type:'PT',submitted:'Jun 25, 10:14 AM',status:'late',compliant:true},
  {name:'Braydon Burnett',type:'TFT',submitted:'—',status:'missing',compliant:false},
  {name:'Errol A. Green',type:'PT',submitted:'Jun 4, 7:58 AM',status:'on-time',compliant:false},
];
function renderAvailMgmt(){
  const el=document.getElementById('avail-mgmt-table');
  if(!el)return;
  el.innerHTML='<thead><tr><th>Name</th><th>Type</th><th>Submitted</th><th>Status</th><th>Compliant</th><th>Action</th></tr></thead><tbody>'+
    availData.map(r=>'<tr><td><b>'+r.name+'</b></td><td>'+r.type+'</td><td>'+r.submitted+'</td><td>'+
      (r.status==='on-time'?'<span class="badge b-act">On time</span>':r.status==='late'?'<span class="badge b-sus">Late — bottom of rotation</span>':'<span class="badge b-ter">Not submitted</span>')+'</td><td>'+
      (r.compliant?'<span style="color:var(--green)">✓ Meets minimum</span>':'<span style="color:var(--red)">✗ Non-compliant — review</span>')+'</td><td>'+
      '<button class="btn sm" onclick="notify(\'Viewing '+r.name+'\\\'s availability sheet.\')">View sheet</button></td></tr>').join('')+'</tbody>';
}

let availMethod='upload';
function setAvailMethod(m,btn){
  availMethod=m;
  document.getElementById('av-upload-btn').style.background='';document.getElementById('av-upload-btn').style.color='';document.getElementById('av-upload-btn').style.borderColor='';
  document.getElementById('av-digital-btn').style.background='';document.getElementById('av-digital-btn').style.color='';document.getElementById('av-digital-btn').style.borderColor='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  document.getElementById('av-upload-area').style.display=m==='upload'?'block':'none';
  document.getElementById('av-digital-area').style.display=m==='digital'?'block':'none';
  if(m==='digital') buildAvailGrid();
}
function buildAvailGrid(){
  const days=['Sun Jun 29','Mon Jun 30','Tue Jul 1','Wed Jul 2','Thu Jul 3','Fri Jul 4','Sat Jul 5','Sun Jul 6','Mon Jul 7','Tue Jul 8','Wed Jul 9','Thu Jul 10','Fri Jul 11','Sat Jul 12'];
  const shifts=['J1 Day','S1 Eve','N Night'];
  let h='<thead><tr><th>Shift</th>'+days.map(d=>'<th style="font-size:9px">'+d.replace(' ','<br>')+'</th>').join('')+'</tr></thead><tbody>';
  shifts.forEach(s=>{
    h+='<tr><td style="white-space:nowrap;font-size:10px;font-weight:600">'+s+'</td>';
    days.forEach((_,i)=>h+='<td style="text-align:center"><input type="checkbox" style="cursor:pointer" title="Click to mark available"></td>');
    h+='</tr>';
  });
  h+='</tbody>';
  document.getElementById('avail-grid-table').innerHTML=h;
}
function handleAvailUpload(input){
  if(input.files.length) notify('File "'+input.files[0].name+'" uploaded. Management will review your availability sheet before the deadline.');
}
function submitAvailabilityOld(){
  const now=new Date();const deadline=new Date('2026-06-25T09:00:00');
  if(now>deadline){notify('⚠️ Submission is past the deadline (Jun 25 at 9:00 AM). You have been placed at the bottom of the rotation for PP 08. Management has been notified.');return;}
  notify('Availability sheet submitted for PP 08. Submitted: '+now.toLocaleString()+'. Email confirmation sent to you and management.');
}

/* ===================== DEADLINES ===================== */
const deadlineData=[
  {title:'PP 08 Availability deadline',date:'Wed Jun 25',time:'9:00 AM',vis:'All staff',notes:'Submit by the deadline or be placed at bottom of rotation.',urgent:true},
  {title:'PP 09 Schedule draft ready for review',date:'Mon Jul 7',time:'',vis:'Management only',notes:'Review and approve before publishing to staff.',urgent:false},
  {title:'Next pay period starts',date:'Sat Jun 28',time:'',vis:'All staff',notes:'PP 08 begins. Ensure all week 3–4 coverage is confirmed.',urgent:false},
  {title:'OT offers close — PP 07',date:'Fri Jun 20',time:'5:00 PM',vis:'Management only',notes:'All outstanding OT offers must be resolved by end of day.',urgent:true},
];
function renderDeadlines(){
  const el=document.getElementById('deadline-list');
  if(!el)return;
  el.innerHTML=deadlineData.map(d=>`
    <div class="card" style="${d.urgent?'border-left:3px solid var(--red)':''}">
      <div style="display:flex;justify-content:space-between;align-items:flex-start">
        <div>
          <div style="font-weight:600;font-size:13px;margin-bottom:3px">${d.urgent?'🔴 ':''}<span>${d.title}</span></div>
          <div style="font-size:12px;color:var(--t2)">📅 ${d.date}${d.time?' at '+d.time:''} &nbsp;·&nbsp; 👁 ${d.vis}</div>
          ${d.notes?'<div style="font-size:11px;color:var(--t3);margin-top:4px">'+d.notes+'</div>':''}
        </div>
        <button class="btn sm red" onclick="this.closest('.card').remove()">Remove</button>
      </div>
    </div>`).join('');
}
function saveDeadline(){
  const title=document.getElementById('dl-title').value||'New reminder';
  const date=document.getElementById('dl-date').value||'TBD';
  const time=document.getElementById('dl-time').value;
  const vis=document.getElementById('dl-vis').value;
  const notes=document.getElementById('dl-notes').value;
  deadlineData.unshift({title,date,time,vis,notes,urgent:false});
  closeModal('new-deadline-modal');renderDeadlines();
  notify('Reminder "'+title+'" added.');
}

/* ===================== AVAILABILITY — SPLIT SHEETS ===================== */
// Management tab switcher
function availMgmtTab(tab,btn){
  ['pt','ot','hist'].forEach(t=>{
    document.getElementById('avmgmt-panel-'+t).style.display='none';
    const b=document.getElementById('avmgmt-tab-'+t);
    b.style.background='';b.style.color='';b.style.borderColor='';
  });
  document.getElementById('avmgmt-panel-'+tab).style.display='block';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  if(tab==='pt') renderAvailPT();
  if(tab==='ot') renderAvailOT();
  if(tab==='hist') renderAvailHistory();
}
// PT & Recall data
const availPTData=[
  {name:'Steven Yearwood',pos:'PT',submitted:'Jun 5, 11:30 AM',status:'on-time',compliant:true,refusals:0},
  {name:'Keon Pompey',pos:'PT',submitted:'Jun 26, 10:14 AM',status:'late',compliant:true,refusals:1},
  {name:'Jema Larose',pos:'PT',submitted:'Jun 4, 8:22 AM',status:'on-time',compliant:true,refusals:0},
  {name:'Chynna Lewis',pos:'PT',submitted:'Jun 3, 7:58 AM',status:'on-time',compliant:false,refusals:0},
  {name:'Gilles Lezi',pos:'Recall',submitted:'Jun 5, 9:02 AM',status:'on-time',compliant:true,refusals:2},
  {name:'Braydon Burnett',pos:'Recall',submitted:'—',status:'missing',compliant:false,refusals:0},
];
function renderAvailPT(){
  const el=document.getElementById('avail-pt-table');if(!el)return;
  el.innerHTML='<thead><tr><th>Name</th><th>Position</th><th>Submitted</th><th>Status</th><th>Compliant</th><th>Refusals PP</th><th>Action</th></tr></thead><tbody>'+
    availPTData.map(r=>'<tr><td><b>'+r.name+'</b></td><td><span class="badge '+(r.pos==='PT'?'b-sus':'b-ter')+'">'+r.pos+'</span></td><td>'+r.submitted+'</td><td>'+
      (r.status==='on-time'?'<span class="badge b-act">On time</span>':r.status==='late'?'<span class="badge b-sus">Late — bottom of list</span>':'<span class="badge b-ter">Not submitted</span>')+'</td><td>'+
      (r.compliant?'<span style="color:var(--green)">✓ Meets minimum</span>':'<span style="color:var(--red)">✗ Non-compliant</span>')+'</td><td>'+
      (r.refusals>=2?'<span style="color:var(--red);font-weight:700">⚠ '+r.refusals+' — flagged</span>':'<span style="color:var(--t2)">'+r.refusals+'</span>')+'</td><td>'+
      '<button class="btn sm" onclick="notify(\'Viewing '+r.name+'\\\'s availability sheet.\')">View sheet</button></td></tr>').join('')+'</tbody>';
}
// OT availability data (FT only)
const availOTData=[
  {name:'Kerwin Guy-Roach',pos:'FT',submitted:'Jun 3, 8:47 AM',status:'on-time'},
  {name:'Ansonia Arrington',pos:'TFT',submitted:'Jun 3, 9:12 AM',status:'on-time'},
  {name:'Keith Burnett',pos:'FT',submitted:'Jun 3, 9:30 AM',status:'on-time'},
  {name:'Greg Page',pos:'FT',submitted:'—',status:'missing'},
  {name:'Paul Vincent',pos:'FT',submitted:'Jun 26, 11:05 AM',status:'late'},
];
function renderAvailOT(){
  const el=document.getElementById('avail-ot-table');if(!el)return;
  el.innerHTML='<thead><tr><th>Name</th><th>Position</th><th>Submitted</th><th>Status</th><th>Action</th></tr></thead><tbody>'+
    availOTData.map(r=>'<tr><td><b>'+r.name+'</b></td><td><span class="badge b-ft">'+r.pos+'</span></td><td>'+r.submitted+'</td><td>'+
      (r.status==='on-time'?'<span class="badge b-act">Submitted</span>':r.status==='late'?'<span class="badge b-sus">Late</span>':'<span class="badge" style="background:var(--bg1);color:var(--t2)">Not submitted</span>')+'</td><td>'+
      '<button class="btn sm" onclick="notify(\'Viewing '+r.name+'\\\'s OT availability sheet.\')">View sheet</button></td></tr>').join('')+'</tbody>';
}
// History (combined view)
const availHistData={
  PP08:[
    {name:'Steven Yearwood',pos:'PT',sheet:'PT/Recall',submitted:'Jun 5',status:'on-time',compliant:true},
    {name:'Kerwin Guy-Roach',pos:'FT',sheet:'OT',submitted:'Jun 3',status:'on-time',compliant:true},
    {name:'Keon Pompey',pos:'PT',sheet:'PT/Recall',submitted:'Jun 26',status:'late',compliant:true},
    {name:'Jema Larose',pos:'PT',sheet:'PT/Recall',submitted:'Jun 4',status:'on-time',compliant:true},
    {name:'Braydon Burnett',pos:'Recall',sheet:'PT/Recall',submitted:'—',status:'missing',compliant:false},
  ],
  PP07:[
    {name:'Steven Yearwood',pos:'PT',sheet:'PT/Recall',submitted:'May 22',status:'on-time',compliant:true},
    {name:'Kerwin Guy-Roach',pos:'FT',sheet:'OT',submitted:'May 20',status:'on-time',compliant:true},
    {name:'Keon Pompey',pos:'PT',sheet:'PT/Recall',submitted:'May 20',status:'on-time',compliant:true},
    {name:'Jema Larose',pos:'PT',sheet:'PT/Recall',submitted:'May 22',status:'on-time',compliant:true},
  ],
  PP06:[
    {name:'Steven Yearwood',pos:'PT',sheet:'PT/Recall',submitted:'May 8',status:'late',compliant:true},
    {name:'Kerwin Guy-Roach',pos:'FT',sheet:'OT',submitted:'—',status:'missing',compliant:true},
    {name:'Keon Pompey',pos:'PT',sheet:'PT/Recall',submitted:'May 7',status:'on-time',compliant:false},
  ]
};
function renderAvailHistory(){
  const pp=document.getElementById('avail-hist-pp')?.value||'PP08';
  const el=document.getElementById('avail-hist-table');if(!el)return;
  const rows=availHistData[pp]||[];
  el.innerHTML='<thead><tr><th>Name</th><th>Position</th><th>Sheet type</th><th>Submitted</th><th>Status</th><th>Compliant</th></tr></thead><tbody>'+
    rows.map(r=>'<tr><td><b>'+r.name+'</b></td><td>'+r.pos+'</td><td><span class="badge '+(r.sheet==='OT'?'b-ft':'b-sus')+'">'+r.sheet+'</span></td><td>'+r.submitted+'</td><td>'+
      (r.status==='on-time'?'<span class="badge b-act">On time</span>':r.status==='late'?'<span class="badge b-sus">Late</span>':'<span class="badge b-ter">Missing</span>')+'</td><td>'+
      (r.compliant?'<span style="color:var(--green)">✓</span>':'<span style="color:var(--red)">✗ Review</span>')+'</td></tr>').join('')+'</tbody>';
}
// Employee submit (shared for both sheet types)
function submitAvailability(type){
  const label=type==='ot'?'OT availability sheet':'Availability sheet';
  const now=new Date();const deadline=new Date('2026-06-25T09:00:00');
  if(now>deadline){
    notify('⚠️ '+label+' submitted past the deadline (Jun 25 at 9:00 AM). '+(type==='pt'?'You have been placed at the bottom of the rotation for PP 08. Management has been notified.':'Your OT sheet has been recorded as late.'));
  } else {
    notify(label+' submitted for PP 08. '+(type==='pt'?'As PT/Recall, you are required to work any shifts you marked available. ':'OT availability recorded — management will contact you in order. ')+' Email confirmation sent.');
  }
}
function setOtAvailMethod(m,btn){
  document.getElementById('ot-upload-btn').style.cssText='';
  document.getElementById('ot-digital-btn').style.cssText='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  document.getElementById('ot-upload-area').style.display=m==='upload'?'block':'none';
  document.getElementById('ot-digital-area').style.display=m==='digital'?'block':'none';
  if(m==='digital'){
    const days=['Sun Jun 29','Mon Jun 30','Tue Jul 1','Wed Jul 2','Thu Jul 3','Fri Jul 4','Sat Jul 5','Sun Jul 6','Mon Jul 7','Tue Jul 8','Wed Jul 9','Thu Jul 10','Fri Jul 11','Sat Jul 12'];
    const shifts=['J1 Day','S1 Eve','N Night'];
    let h='<thead><tr><th>Shift</th>'+days.map(d=>'<th style="font-size:9px">'+d.replace(' ','<br>')+'</th>').join('')+'</tr></thead><tbody>';
    shifts.forEach(s=>{h+='<tr><td style="white-space:nowrap;font-size:10px;font-weight:600">'+s+'</td>';days.forEach(()=>h+='<td style="text-align:center"><input type="checkbox" style="cursor:pointer"></td>');h+='</tr>';});
    h+='</tbody>';
    document.getElementById('ot-avail-grid-table').innerHTML=h;
  }
}
function handleOtUpload(input){if(input.files.length) notify('OT availability sheet "'+input.files[0].name+'" uploaded.');}

/* ===================== ON-CALL ===================== */
function oncallTab(tab,btn){
  ['pkg','bookoffs'].forEach(t=>{
    document.getElementById('oncall-panel-'+t).style.display='none';
    const b=document.getElementById('oncall-tab-'+t);
    b.style.background='';b.style.color='';b.style.borderColor='';
  });
  document.getElementById('oncall-panel-'+tab).style.display='block';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  if(tab==='bookoffs') renderOncallBookoffs();
}
// Priority list logic: PT < 10 shifts first, then Recall < 10, then FT OT (10+)
const oncallEmpPool={
  'sat-s1':[
    {name:'Jema Larose',pos:'PT',shifts:9,avail:true,refusals:0},
    {name:'Chynna Lewis',pos:'PT',shifts:5,avail:true,refusals:0},
    {name:'Gilles Lezi',pos:'Recall',shifts:5,avail:true,refusals:2},
    {name:'Kerwin Guy-Roach',pos:'FT',shifts:10,avail:true,refusals:0},
    {name:'Ansonia Arrington',pos:'TFT',shifts:10,avail:true,refusals:0},
  ],
  'fri-n':[
    {name:'Steven Yearwood',pos:'PT',shifts:8,avail:true,refusals:1},
    {name:'Keon Pompey',pos:'Recall',shifts:4,avail:true,refusals:0},
    {name:'Greg Page',pos:'FT',shifts:11,avail:true,refusals:0},
  ],
  'wed-j1':[
    {name:'Chynna Lewis',pos:'PT',shifts:5,avail:true,refusals:0},
    {name:'Gilles Lezi',pos:'Recall',shifts:5,avail:true,refusals:2},
    {name:'Keith Burnett',pos:'FT',shifts:10,avail:true,refusals:0},
  ]
};
function renderOncallPackage(){
  const shift=document.getElementById('oncall-shift-select').value;
  const el=document.getElementById('oncall-package-table');
  if(!shift){el.innerHTML='';return;}
  const pool=oncallEmpPool[shift]||[];
  // Sort: PT < 10 first (by shifts asc), then Recall < 10 (by shifts asc), then 10+
  const ptShort=pool.filter(e=>e.pos==='PT'&&e.shifts<10).sort((a,b)=>a.shifts-b.shifts);
  const rcShort=pool.filter(e=>e.pos==='Recall'&&e.shifts<10).sort((a,b)=>a.shifts-b.shifts);
  const ot=pool.filter(e=>e.shifts>=10||e.pos==='FT'||e.pos==='TFT');
  const sorted=[...ptShort,...rcShort,...ot];
  const posColor={PT:'var(--amberlight)',Recall:'var(--redlight)',FT:'var(--bluelight)',TFT:'var(--teallight)'};
  const posText={PT:'var(--amber)',Recall:'var(--red)',FT:'var(--blue)',TFT:'var(--teal)'};
  let i=1;
  el.innerHTML='<div class="info" style="margin-bottom:.75rem">📋 Offer order for selected shift — management eyes only. PT (under 10 shifts) → Recall (under 10 shifts) → Full-time / OT list.</div>'+
    '<table class="bt"><thead><tr><th>#</th><th>Name</th><th>Position</th><th>Shifts this PP</th><th>Available</th><th>PP Refusals</th><th>Action</th></tr></thead><tbody>'+
    sorted.map(e=>{
      const isOT=e.shifts>=10;
      const flag=e.refusals>=2?'<span style="color:var(--red);font-size:10px;font-weight:700"> ⚠ flagged</span>':'';
      const obligated=!isOT&&(e.pos==='PT'||e.pos==='Recall');
      return '<tr style="'+(i===1?'background:var(--greenlight)':isOT?'background:var(--bluelight)':'')+'"><td><b>'+i+++'</b></td><td><b>'+e.name+'</b></td><td><span class="badge" style="background:'+posColor[e.pos]+';color:'+posText[e.pos]+'">'+e.pos+'</span></td><td>'+(isOT?'<span style="color:var(--blue)">'+e.shifts+' (OT territory)</span>':'<b>'+e.shifts+'</b>')+'</td><td>'+(e.avail?'<span style="color:var(--green)">✓ Available</span>':'<span style="color:var(--t3)">Not available</span>')+'</td><td>'+e.refusals+flag+'</td><td>'+
        '<button class="btn sm grn" onclick="logOncallOffer(\''+e.name+'\',\''+e.pos+'\',\''+e.shifts+'\','+obligated+')">Offer shift</button></td></tr>';
    }).join('')+'</tbody></table>';
}
function logOncallOffer(name,pos,shifts,obligated){
  const msg=obligated
    ? 'Shift offered to '+name+' ('+pos+', '+shifts+' shifts). As PT/Recall on availability, they are required to accept. App notification + call required. Refusal will be documented.'
    : 'OT shift offered to '+name+' ('+pos+', '+shifts+' shifts). Employee may accept or decline. Response required within 1 hour.';
  notify(msg);
}
function addToShift(){
  const emp=document.getElementById('oncall-add-emp').value;
  const shift=document.getElementById('oncall-add-shift').value;
  notify(emp+' added to '+shift+'. Schedule updated live. Staff will see update at next Mon/Wed/Fri push by scheduler.');
}
// Book-off requests
const bookoffRequests=[
  {emp:'Paul Vincent',date:'Jun 20',shift:'S1 Eve',unit:'Boys IA',reason:'Family emergency',submitted:'Jun 20, 6:12 PM',status:'pending'},
];
const bookoffHistory=[
  {emp:'Kerwin Guy-Roach',date:'Jun 14',shift:'J1 Day',unit:'Girls Educators',reason:'Sick',submitted:'Jun 14, 5:48 PM',status:'approved'},
  {emp:'Shannon Ridley',date:'Jun 17',shift:'S1 Eve',unit:'Boys Educators',reason:'Vacation',submitted:'Jun 17, 5:02 PM',status:'approved'},
];
function renderOncallBookoffs(){
  const el=document.getElementById('oncall-bookoff-table');
  const el2=document.getElementById('oncall-bookoff-hist');
  if(!el||!el2)return;
  el.innerHTML='<thead><tr><th>Employee</th><th>Date / Shift</th><th>Unit</th><th>Reason</th><th>Submitted</th><th>Action</th></tr></thead><tbody>'+
    bookoffRequests.map((r,i)=>'<tr><td><b>'+r.emp+'</b></td><td>'+r.date+' · '+r.shift+'</td><td>'+r.unit+'</td><td>'+r.reason+'</td><td>'+r.submitted+'</td><td><button class="btn sm grn" onclick="resolveBookoff('+i+',\'approved\')">Approve</button> <button class="btn sm red" onclick="resolveBookoff('+i+',\'denied\')">Deny</button></td></tr>').join('')+'</tbody>';
  el2.innerHTML='<thead><tr><th>Employee</th><th>Date / Shift</th><th>Unit</th><th>Reason</th><th>Submitted</th><th>Status</th></tr></thead><tbody>'+
    bookoffHistory.map(r=>'<tr><td><b>'+r.emp+'</b></td><td>'+r.date+' · '+r.shift+'</td><td>'+r.unit+'</td><td>'+r.reason+'</td><td>'+r.submitted+'</td><td><span class="badge '+(r.status==='approved'?'b-act':'b-ter')+'">'+r.status+'</span></td></tr>').join('')+'</tbody>';
}
function resolveBookoff(i,decision){
  const r=bookoffRequests[i];
  bookoffHistory.unshift({...r,status:decision});
  bookoffRequests.splice(i,1);
  renderOncallBookoffs();
  notify('Book-off '+decision+' for '+r.emp+' ('+r.date+' · '+r.shift+'). Employee notified by app + call required. Replacement package ready under Replacement package tab.');
}

/* ===================== SHIFT ROSTER ===================== */
const rosterEmps=[
  {name:'Kerwin Guy-Roach',pos:'FT',unit:'Girls Educators',sen:'2015-04-12'},
  {name:'Ansonia Arrington',pos:'TFT',unit:'Boys Educators',sen:'2016-06-08'},
  {name:'Steven Yearwood',pos:'PT',unit:'Girls IA',sen:'2018-09-01'},
  {name:'Keon Pompey',pos:'PT',unit:'Boys IA',sen:'2019-03-14'},
  {name:'Jema Larose',pos:'PT',unit:'Girls IA',sen:'2020-01-22'},
  {name:'Chynna Lewis',pos:'PT',unit:'Boys IA',sen:'2021-07-05'},
  {name:'Gilles Lezi',pos:'Recall',unit:'Boys Educators',sen:'2022-02-18'},
  {name:'Keith Burnett',pos:'FT',unit:'Boys IA',sen:'2014-11-30'},
  {name:'Greg Page',pos:'FT',unit:'Girls Educators',sen:'2013-08-27'},
];
const coverageLog=[
  {emp:'Keith Burnett',date:'Jun 20',shift:'S1 Eve',unit:'Boys IA',notes:'OT cover'},
  {emp:'Gilles Lezi',date:'Jun 17',shift:'N Night',unit:'Boys Educators',notes:'Emergency replacement'},
  {emp:'Greg Page',date:'Jun 15',shift:'J1 Day',unit:'Boys Educators',notes:'OT cover'},
];
function renderRoster(){
  const el=document.getElementById('roster-emp-table');if(!el)return;
  const posColor={FT:'b-ft',TFT:'b-act',PT:'b-sus',Recall:'b-ter'};
  el.innerHTML='<thead><tr><th>Name</th><th>Position</th><th>Unit</th><th>Seniority date</th><th></th></tr></thead><tbody>'+
    rosterEmps.map((r,i)=>'<tr><td><b>'+r.name+'</b></td><td><span class="badge '+posColor[r.pos]+'">'+r.pos+'</span></td><td>'+r.unit+'</td><td style="font-size:11px;color:var(--t2)">'+r.sen+'</td><td><button class="btn sm red" onclick="removeRosterEmp('+i+')">Remove</button></td></tr>').join('')+'</tbody>';
  const el2=document.getElementById('roster-coverage-table');if(!el2)return;
  el2.innerHTML='<thead><tr><th>Employee</th><th>Date</th><th>Shift</th><th>Unit</th><th>Notes</th></tr></thead><tbody>'+
    coverageLog.map(r=>'<tr><td><b>'+r.emp+'</b></td><td>'+r.date+'</td><td>'+r.shift+'</td><td>'+r.unit+'</td><td style="font-size:11px;color:var(--t2)">'+r.notes+'</td></tr>').join('')+'</tbody>';
}
function removeRosterEmp(i){const n=rosterEmps[i].name;rosterEmps.splice(i,1);renderRoster();notify(n+' removed from roster.');}
function saveRosterEmp(){
  const name=document.getElementById('roster-name').value;if(!name){notify('Please enter a name.');return;}
  rosterEmps.push({name,pos:document.getElementById('roster-pos').value,unit:document.getElementById('roster-unit').value,sen:document.getElementById('roster-sendate').value||'—'});
  closeModal('add-roster-modal');renderRoster();notify(name+' added to master roster.');
}
function saveCoverage(){
  const emp=document.getElementById('cov-emp').value;
  coverageLog.unshift({emp,date:document.getElementById('cov-date').value||'—',shift:document.getElementById('cov-shift').value,unit:document.getElementById('cov-unit').value,notes:document.getElementById('cov-notes').value||'—'});
  closeModal('add-coverage-modal');renderRoster();notify('Coverage recorded: '+emp+' — '+document.getElementById('cov-shift').value+'.');
}

/* ===================== SCHEDULE PUSH (Mon/Wed/Fri) ===================== */
const schedPushLog=[
  {date:'Mon Jun 16',time:'8:00 AM',desc:'Boys IA (Day/Eve) — OT cover added Week 2',by:'Scheduling Admin'},
  {date:'Wed Jun 18',time:'8:01 AM',desc:'Boys Educators — OT assignments + switch confirmed',by:'Scheduling Admin'},
  {date:'Fri Jun 20',time:'8:03 AM',desc:'All 6 schedules — Week 2 final + Week 3 preview',by:'Unit Manager'},
];
function pushScheduleUpdate(){
  const now=new Date();
  const ts=now.toLocaleString('en-CA',{weekday:'short',month:'short',day:'numeric',hour:'2-digit',minute:'2-digit'});
  const day=now.toLocaleDateString('en-CA',{weekday:'long'});
  const sendDays=['Monday','Wednesday','Friday'];
  if(!sendDays.includes(day)){
    if(!confirm('Today is '+day+'. Schedule updates are normally sent Mon/Wed/Fri. Send anyway?')) return;
  }
  schedPushLog.unshift({date:ts.split(',')[0],time:ts.split(',')[1]?.trim()||'',desc:'Schedule update — manual push',by:'Scheduling Admin'});
  renderSchedPushLog();
  notify('✅ Schedule update sent '+ts+'. All staff notified by in-app notification + email. On-call manager copied. Next push day: '+sendDays.find(d=>d>day)||'Monday');
}
function renderSchedPushLog(){
  const el=document.getElementById('sched-push-log');if(!el)return;
  el.innerHTML='<thead><tr><th>Date</th><th>Time</th><th>Changes</th><th>Published by</th></tr></thead><tbody>'+
    schedPushLog.map(r=>'<tr><td><b>'+r.date+'</b></td><td>'+r.time+'</td><td>'+r.desc+'</td><td>'+r.by+'</td></tr>').join('')+'</tbody>';
}

/* ===================== NOTIFICATIONS ===================== */
function notify(msg){
  const el=document.createElement('div');
  el.style.cssText='background:var(--bg2);border:1px solid var(--greenmid);border-left:3px solid var(--green);border-radius:var(--r);padding:10px 12px;font-size:12px;margin-bottom:6px;box-shadow:0 2px 8px rgba(0,0,0,.1);line-height:1.4';
  el.innerHTML='<b style="color:var(--green)">✓ Done</b><br>'+msg;
  document.getElementById('notif-wrap').prepend(el);
  setTimeout(()=>el.remove(),5000);
}

/* ===================== SENIORITY — SPLIT EDUCATORS / IA ===================== */
let currentSenUnit='educators';
function senTab(unit, btn){
  currentSenUnit=unit;
  document.querySelectorAll('#sen-tab-ed,#sen-tab-ia').forEach(b=>{b.style.background='';b.style.color='';b.style.borderColor='';});
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  const label=unit==='educators'?'Educators':'Intervention Agents';
  document.getElementById('sen-unit-label').textContent=label+' — Seniority List';
  renderSenNew();
}
function renderSenNew(){
  const list=senData[currentSenUnit];
  document.getElementById('sen-list').innerHTML=list.map((s,i)=>`
    <li class="sen-row" draggable="true" ondragstart="dragStart(${i})" ondragover="event.preventDefault()" ondrop="dragDrop(event,${i})" ondragend="dragEnd()">
      <span style="color:var(--t3);font-size:16px;cursor:grab">≡</span>
      <span class="sen-rank">${i+1}</span>
      <span class="sen-name">${s.name}</span>
      <span class="sen-meta">${s.title||s.status} · ${s.status} · ${s.years}</span>
      <button class="arr btn" style="font-size:11px;padding:3px 7px;background:var(--red10);color:#c0392b;border:1px solid #f5c6cb" onclick="removeSenStaff('${currentSenUnit}',${i})">Remove</button>
    </li>`).join('');
}
function renameSenUnit(){
  const label=currentSenUnit==='educators'?'Educators':'Intervention Agents';
  const name=prompt('Rename "'+label+'" to:',label);
  if(name&&name.trim()) notify('Unit renamed to "'+name.trim()+'" — reflected across the app.');
}
function removeSenStaff(unit,i){
  if(!confirm('Remove '+senData[unit][i].name+' from seniority list?')) return;
  senData[unit].splice(i,1);
  renderSenNew();
  notify('Staff member removed from seniority list.');
}
function addSenStaff(){
  const name=document.getElementById('sen-new-name').value.trim();
  const titleEl=document.getElementById('sen-new-title');
  const title=titleEl.options[titleEl.selectedIndex].text;
  const val=titleEl.value;
  const unit=(val==='ed'||val==='ed2')?'educators':'ia';
  const pos=document.getElementById('sen-new-pos').value;
  const date=document.getElementById('sen-new-date').value;
  if(!name){alert('Please enter a name.');return;}
  senData[unit].push({name,title,status:pos,years:date?'Since '+date:'New hire'});
  closeModal('add-sen-modal');
  currentSenUnit=unit;
  const btn=document.getElementById(unit==='educators'?'sen-tab-ed':'sen-tab-ia');
  senTab(unit,btn);
  notify('Added '+name+' to '+unit+' seniority list as '+title+'.');
}

/* ===================== STAFF PROFILES ===================== */
const empProfileData=[
  {name:'Keith Burnett',type:'FT',unit:'Boys IA',pickups:3,refusals:1,bookoffs:0,ot:5,lateSubmit:0,earlyLeave:1,earlyReason:'Family emergency',shifts:14,recall:0,pt:0},
  {name:"Mark D'Agostino",type:'FT',unit:'Boys IA',pickups:1,refusals:0,bookoffs:1,ot:2,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:12,recall:0,pt:0},
  {name:'Greg Page',type:'FT',unit:'Boys IA',pickups:4,refusals:2,bookoffs:0,ot:7,lateSubmit:1,earlyLeave:0,earlyReason:'',shifts:14,recall:0,pt:0},
  {name:'Jean-Nicolas Michaud',type:'FT',unit:'Boys IA',pickups:0,refusals:0,bookoffs:2,ot:1,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:12,recall:0,pt:0},
  {name:'Steven Yearwood',type:'PT',unit:'Boys IA',pickups:2,refusals:0,bookoffs:0,ot:0,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:8,recall:0,pt:8},
  {name:'Keon Pompey',type:'PT',unit:'Boys IA',pickups:1,refusals:3,bookoffs:1,ot:0,lateSubmit:1,earlyLeave:0,earlyReason:'',shifts:7,recall:0,pt:7},
  {name:'Gilles Lezi',type:'FT',unit:'Boys Ed',pickups:2,refusals:0,bookoffs:0,ot:3,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:13,recall:0,pt:0},
  {name:'Ansonia Arrington',type:'TFT',unit:'Girls Ed',pickups:1,refusals:1,bookoffs:0,ot:4,lateSubmit:0,earlyLeave:1,earlyReason:'Medical appointment',shifts:11,recall:0,pt:0},
  {name:'Shannon Ridley',type:'PT',unit:'Girls Ed',pickups:0,refusals:0,bookoffs:0,ot:0,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:9,recall:0,pt:9},
  {name:'Yvonne Kaberamanzi',type:'Recall',unit:'Girls Ed',pickups:3,refusals:0,bookoffs:0,ot:0,lateSubmit:0,earlyLeave:0,earlyReason:'',shifts:6,recall:6,pt:0},
];
function renderEmpProfileList(){
  const tbody=document.getElementById('profile-emp-table');
  tbody.innerHTML='<thead><tr><th>Name</th><th>Type</th><th>Unit</th><th>Shifts PP</th><th>OT shifts</th><th>Refusals</th><th>Book-offs</th></tr></thead><tbody>'+
    empProfileData.map((e,i)=>`<tr onclick="showEmpProfile(${i})" style="cursor:pointer">
      <td><b>${e.name}</b></td><td>${e.type}</td><td>${e.unit}</td>
      <td>${e.shifts}</td>
      <td>${e.ot>=4?`<b style="color:#c0392b">${e.ot} ⚠</b>`:e.ot}</td>
      <td>${e.refusals>=2?`<b style="color:#c0392b">${e.refusals} 🚩</b>`:e.refusals}</td>
      <td>${e.bookoffs}</td>
    </tr>`).join('')+'</tbody>';
}
function showEmpProfile(i){
  const e=empProfileData[i];
  document.getElementById('profile-list-view').style.display='none';
  document.getElementById('profile-detail-view').style.display='';
  const otFlag=e.ot>=4?`<span style="background:#FFF3F3;border:1px solid #f5c6cb;color:#c0392b;border-radius:4px;padding:2px 8px;font-size:11px;font-weight:700">⚠ HIGH OT — ${e.ot} shifts</span>`:`<span style="background:var(--bluelight);color:var(--blue);border-radius:4px;padding:2px 8px;font-size:11px">${e.ot} OT shifts</span>`;
  const refFlag=e.refusals>=2?`<span style="background:#FFF3F3;border:1px solid #f5c6cb;color:#c0392b;border-radius:4px;padding:2px 8px;font-size:11px;font-weight:700">🚩 ${e.refusals} refusals — management alert</span>`:`${e.refusals} refusals`;
  document.getElementById('profile-detail-content').innerHTML=`
    <div class="card">
      <div class="card-title">${e.name} — ${e.type} · ${e.unit}</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:1rem">${otFlag}</div>
      <table class="bt" style="font-size:12px"><tbody>
        <tr><td><b>Shift pickups (PP)</b></td><td>${e.pickups}</td></tr>
        <tr><td><b>Refusals (PP)</b></td><td>${refFlag}</td></tr>
        <tr><td><b>Book-offs (PP)</b></td><td>${e.bookoffs}</td></tr>
        <tr><td><b>OT shifts (PP)</b></td><td>${e.ot}</td></tr>
        <tr><td><b>Late availability submission</b></td><td>${e.lateSubmit>0?`<span style="color:#c0392b">${e.lateSubmit} late</span>`:'None'}</td></tr>
        <tr><td><b>Left shift early</b></td><td>${e.earlyLeave>0?`${e.earlyLeave}× — Reason: ${e.earlyReason||'not recorded'}`:'None'}</td></tr>
      </tbody></table>
      <div style="margin-top:1rem;font-weight:600;font-size:12px">Regular shifts breakdown</div>
      <table class="bt" style="font-size:12px"><tbody>
        <tr><td><b>Total shifts this PP</b></td><td>${e.shifts} ${e.shifts>=10?'<span style="color:var(--green);font-weight:700">✓ Full (10+)</span>':'<span style="color:#c0392b">⚠ Under 10</span>'}</td></tr>
        <tr><td><b>Recall shifts</b></td><td>${e.recall}</td></tr>
        <tr><td><b>PT shifts</b></td><td>${e.pt}</td></tr>
      </tbody></table>
    </div>`;
}
function filterProfileList(){
  const q=document.getElementById('profile-search').value.toLowerCase();
  document.querySelectorAll('#profile-emp-table tbody tr').forEach(r=>{
    r.style.display=r.textContent.toLowerCase().includes(q)?'':'none';
  });
}

/* ===================== LOAN OF SERVICE ===================== */
let loanData=[
  {emp:'Ansonia Arrington',community:'Kuujjuaq Health Centre',weeks:6,start:'2026-06-01',end:'2026-07-13',notes:'Supporting youth crisis unit.',status:'Active'},
];
function renderLoanList(){
  const el=document.getElementById('loan-list');
  if(!loanData.length){el.innerHTML='<p style="color:var(--t3);font-size:13px">No active loans of service.</p>';return;}
  el.innerHTML=loanData.map((l,i)=>`
    <div class="card" style="border-left:3px solid var(--amber)">
      <div class="card-title">${l.emp} — On loan to <b>${l.community}</b></div>
      <table class="bt" style="font-size:12px"><tbody>
        <tr><td>Duration</td><td>${l.weeks} weeks</td></tr>
        <tr><td>Start</td><td>${l.start}</td></tr>
        <tr><td>Estimated return</td><td>${l.end}</td></tr>
        <tr><td>Notes</td><td>${l.notes}</td></tr>
        <tr><td>Status</td><td><span style="color:var(--amber);font-weight:700">${l.status}</span></td></tr>
      </tbody></table>
      <button class="btn" style="margin-top:.5rem;font-size:11px" onclick="endLoan(${i})">Mark returned / end loan</button>
    </div>`).join('');
}
function saveLoan(){
  const emp=document.getElementById('loan-emp').value;
  const community=document.getElementById('loan-community').value.trim();
  const weeks=document.getElementById('loan-weeks').value;
  const start=document.getElementById('loan-start').value;
  const end=document.getElementById('loan-end').value;
  const notes=document.getElementById('loan-notes').value.trim();
  if(!community||!start){alert('Please fill in community and start date.');return;}
  loanData.push({emp,community,weeks,start,end,notes:notes||'—',status:'Active'});
  closeModal('new-loan-modal');
  renderLoanList();
  addEmpNotif(emp,'loan',`You have been placed on a loan of service to <b>${community}</b> starting ${start} for approximately ${weeks} weeks. You have been removed from the UTHC schedule for this period. Contact your manager with any questions.`);
  notify(`Loan of service created for ${emp}. Notifications sent to employee, scheduler, and management.`);
}
function endLoan(i){
  loanData[i].status='Returned';
  renderLoanList();
  notify('Loan of service ended — '+loanData[i].emp+' returned to UTHC schedule.');
}

/* ===================== REGULAR CONTACT LOG ===================== */
let regContactData=[
  {shift:'Sat Jun 21 · S1 (15:00–22:45) · Boys IA',reason:'Book-off — Keon Pompey (SICK)',chain:[
    {name:'Steven Yearwood',contacted:'09:15',outcome:'No answer',status:'moved'},
    {name:'Yvonne Kaberamanzi',contacted:'09:22',outcome:'Refused',status:'moved'},
    {name:'Shannon Ridley',contacted:'09:30',outcome:'',status:'pending'},
  ]},
];
function renderRegContact(){
  const tbody=document.getElementById('regcontact-table');
  if(!regContactData.length){tbody.innerHTML='<tr><td colspan="5" style="color:var(--t3);padding:16px">No contact chains active.</td></tr>';return;}
  let rows='<thead><tr><th>Shift</th><th>Reason</th><th>Contact</th><th>Time contacted</th><th>Outcome / Status</th></tr></thead><tbody>';
  regContactData.forEach((chain,ci)=>{
    rows+=`<tr style="background:var(--bluelight)"><td colspan="5" style="font-weight:600;font-size:12px">📋 ${chain.shift} — ${chain.reason}</td></tr>`;
    chain.chain.forEach((c,i)=>{
      const isPending=c.status==='pending';
      rows+=`<tr>
        <td></td><td></td>
        <td><b>${c.name}</b></td>
        <td>${c.contacted||'—'} <button class="btn" style="font-size:10px;padding:2px 6px" onclick="logRegContactTime(${ci},${i})">Log time</button></td>
        <td>${isPending
          ?`<span style="color:var(--amber);font-weight:700">⏳ Awaiting response</span>
             <button class="btn" style="font-size:10px;padding:2px 6px;margin-left:4px" onclick="logRegAction(${ci},${i},'Answered — accepted')">Accepted</button>
             <button class="btn" style="font-size:10px;padding:2px 6px" onclick="logRegAction(${ci},${i},'Refused')">Refused</button>
             <button class="btn" style="font-size:10px;padding:2px 6px" onclick="logRegAction(${ci},${i},'No answer')">No answer</button>`
          :c.status==='moved'
            ?`<span style="font-size:10px;color:var(--t3)">Moved on → ${chain.chain[i+1]?chain.chain[i+1].name:'(end of list)'}</span>`
            :`<span style="color:var(--green);font-weight:700">✓ ${c.outcome}</span>`
        }</td>
      </tr>`;
    });
    rows+=`<tr><td colspan="5" style="padding:4px 8px"><button class="btn" style="font-size:11px" onclick="addRegContact(${ci})">+ Add next contact</button></td></tr>`;
  });
  rows+='</tbody>';
  tbody.innerHTML=rows;
}
function logRegContactTime(ci,i){
  const t=prompt('Enter time contacted (e.g. 09:45):','');
  if(t){regContactData[ci].chain[i].contacted=t;renderRegContact();}
}
function logRegAction(ci,i,outcome){
  regContactData[ci].chain[i].outcome=outcome;
  regContactData[ci].chain[i].status=outcome==='Answered — accepted'?'accepted':'moved';
  renderRegContact();
}
function addRegContact(ci){
  const name=prompt('Name of next contact:','');
  if(name){regContactData[ci].chain.push({name:name.trim(),contacted:'',outcome:'',status:'pending'});renderRegContact();}
}
function startRegContact(){
  const shift=document.getElementById('rc-shift').value.trim();
  const reason=document.getElementById('rc-reason').value.trim();
  if(!shift){alert('Enter the shift details.');return;}
  regContactData.push({shift,reason:reason||'Shift open',chain:[{name:'—',contacted:'',outcome:'',status:'pending'}]});
  closeModal('new-regcontact-modal');
  renderRegContact();
  notify('New regular contact chain started for: '+shift);
}

/* ===================== DROP SHIFT ===================== */
let dropRequestData=[
  {emp:'Keon Pompey',shift:'Mon Jun 23 · J1 Day · Boys IA',type:'block',code:'SICK',reason:'',status:'pending',submitted:'Jun 20 10:15'},
  {emp:'Shannon Ridley',shift:'Sat Jun 21 · S1 Eve · Boys Ed',type:'pickup',code:'',reason:'',status:'pending',submitted:'Jun 20 11:40'},
];
function renderDropMgmt(){
  const pending=dropRequestData.filter(d=>d.status==='pending');
  const hist=dropRequestData.filter(d=>d.status!=='pending');
  const pendTable=document.getElementById('drop-mgmt-table');
  const histTable=document.getElementById('drop-hist-table');
  pendTable.innerHTML='<thead><tr><th colspan="6" style="background:var(--bluelight);color:var(--blue)">Pending drop requests ('+pending.length+')</th></tr><tr><th>Employee</th><th>Shift</th><th>Type</th><th>Code</th><th>Submitted</th><th>Action</th></tr></thead><tbody>'+
    (pending.length?pending.map((d,i)=>`<tr>
      <td><b>${d.emp}</b></td><td style="font-size:11px">${d.shift}</td>
      <td><span class="badge ${d.type==='block'?'b-ft':'b-pt'}">${d.type==='block'?'Block shift':d.type==='pickup'?'OT pickup':'Non-block'}</span></td>
      <td>${d.code||'—'}</td><td style="font-size:11px">${d.submitted}</td>
      <td>
        <button class="btn" style="background:var(--green10);color:var(--green);border:1px solid var(--greenmid);font-size:11px" onclick="approveDropShift(${dropRequestData.indexOf(d)})">Approve</button>
        <button class="btn" style="background:var(--red10);color:#c0392b;border:1px solid #f5c6cb;font-size:11px" onclick="denyDropShift(${dropRequestData.indexOf(d)})">Deny</button>
      </td>
    </tr>`).join(''):'<tr><td colspan="6" style="color:var(--t3);padding:12px">No pending requests.</td></tr>')+'</tbody>';
  histTable.innerHTML='<thead><tr><th colspan="5" style="background:var(--bg2)">History</th></tr><tr><th>Employee</th><th>Shift</th><th>Code</th><th>Submitted</th><th>Decision</th></tr></thead><tbody>'+
    (hist.length?hist.map(d=>`<tr>
      <td>${d.emp}</td><td style="font-size:11px">${d.shift}</td><td>${d.code||'—'}</td><td style="font-size:11px">${d.submitted}</td>
      <td><span style="color:${d.status==='approved'?'var(--green)':'#c0392b'};font-weight:700">${d.status==='approved'?'✓ Approved':'✗ Denied'}</span></td>
    </tr>`).join(''):'<tr><td colspan="5" style="color:var(--t3);padding:12px">No history yet.</td></tr>')+'</tbody>';
}
function approveDropShift(i){dropRequestData[i].status='approved';renderDropMgmt();notify('Drop request approved for '+dropRequestData[i].emp+'.');}
function denyDropShift(i){dropRequestData[i].status='denied';renderDropMgmt();notify('Drop request denied for '+dropRequestData[i].emp+'.');}

/* ===================== EMPLOYEE DROP SHIFT ===================== */
function selDropLeave(el,val){
  document.querySelectorAll('#drop-code-area .ltab').forEach(t=>t.classList.remove('on'));
  el.classList.add('on');
  const h=document.getElementById('drop-leave-code');
  if(h) h.value=val;
}
function checkDropCode(){
  const sel=document.getElementById('drop-shift-sel');
  const type=sel.value;
  const codeArea=document.getElementById('drop-code-area');
  const noReason=document.getElementById('drop-noreason-area');
  // block shift = leave code required; OT pickup = no reason; non-block = no reason
  if(type==='block'){
    codeArea.style.display='';
    noReason.style.display='none';
  } else {
    codeArea.style.display='none';
    noReason.style.display='';
  }
}
function submitDropShift(){
  const sel=document.getElementById('drop-shift-sel');
  const type=sel.value;
  const shiftText=sel.options[sel.selectedIndex].text;
  let code='';
  if(type==='block'){
    const codeEl=document.getElementById('drop-leave-code');
    code=codeEl?codeEl.value:'';
    if(!code){alert('Please select a leave code for block shifts.');return;}
  }
  dropRequestData.push({emp:'Keith Burnett',shift:shiftText,type,code,reason:'',status:'pending',submitted:'Now'});
  notify('Drop request submitted for: '+shiftText+(code?' ('+code+')':''));
}

/* ===================== EMPLOYEE NOTIFICATIONS ===================== */
let empNotifData=[
  {type:'shift',msg:'<b>Shift assigned:</b> Your availability indicates you are available for <b>Wed Jun 25 · J1 Day · Boys IA</b>. This shift has been added to your schedule.',read:false,ts:'Mon Jun 23'},
  {type:'schedule',msg:'<b>Schedule updated:</b> The schedule for Pay Period 13 has been pushed. Please review your updated shifts.',read:false,ts:'Mon Jun 23'},
  {type:'memo',msg:'<b>Transport shift notice:</b> You have been assigned a transport escort on <b>Thu Jun 26 · TRAN</b>. Please see the Memos tab for details.',read:true,ts:'Fri Jun 20'},
];
function addEmpNotif(emp, type, msg){
  empNotifData.unshift({type,msg,read:false,ts:'Now'});
  const badge=document.querySelector('#emp-nav .nav-badge');
  if(badge){badge.textContent=parseInt(badge.textContent||0)+1;}
}
function renderNotifInbox(){
  const el=document.getElementById('notif-inbox');
  if(!empNotifData.length){el.innerHTML='<p style="color:var(--t3);font-size:13px">No notifications.</p>';return;}
  const typeIcon={shift:'📋',schedule:'📅',memo:'📢',loan:'✈️',bookoff:'📝'};
  el.innerHTML=empNotifData.map((n,i)=>`
    <div style="background:${n.read?'var(--bg2)':'var(--bluelight)'};border:1px solid ${n.read?'var(--bd2)':'#85B7EB'};border-radius:var(--r);padding:10px 14px;margin-bottom:6px;font-size:12px;display:flex;gap:10px;align-items:flex-start">
      <span style="font-size:18px;line-height:1">${typeIcon[n.type]||'🔔'}</span>
      <div style="flex:1">${n.msg}<div style="color:var(--t3);font-size:11px;margin-top:4px">${n.ts}</div></div>
      ${n.read?'':'<button class="btn" style="font-size:10px;padding:2px 6px;white-space:nowrap" onclick="markRead('+i+')">Mark read</button>'}
    </div>`).join('');
}
function markRead(i){empNotifData[i].read=true;renderNotifInbox();}
function markAllRead(){empNotifData.forEach(n=>n.read=true);renderNotifInbox();notify('All notifications marked as read.');}

/* ===================== CELL EDIT (SCHEDULE GRID) ===================== */
let activeCellEl=null;
let activeCellStaffList=null; // which staff list was active when modal opened
function openCellEdit(el, shiftLabel){
  activeCellEl=el;
  document.getElementById('cell-edit-info').textContent='Editing: '+shiftLabel;
  const si=el.dataset&&el.dataset.si!==undefined?parseInt(el.dataset.si):undefined;
  const idx=el.dataset&&el.dataset.idx!==undefined?parseInt(el.dataset.idx):undefined;
  // pull override first, then fall back to base staff array data
  const ov=(si!==undefined&&idx!==undefined)?cellOverrides[si+'-'+idx]||{}:{};
  const staffList=currentGridStaff||schedStaffIA;
  const s=(si!==undefined)?staffList[si]:null;
  // base data from staff arrays
  const baseRaw=s&&s.cells&&s.cells[idx]?s.cells[idx]:'';
  const baseShift=baseRaw.replace(/\s*(sw|\/T)\s*/gi,'').trim();
  const baseBookoff=s&&s.bookoff&&s.bookoff[idx]?s.bookoff[idx]:'';
  const baseCover=s&&s.cover&&s.cover[idx]?s.cover[idx]:'';
  // resolved values: override wins over base
  const resolvedShift=ov.shift||baseShift;
  const resolvedBookoff=ov.bookoff||baseBookoff;
  const resolvedCover=ov.name||baseCover;
  const resolvedStart=ov.start||'';
  const resolvedEnd=ov.end||'';
  // fill time fields
  document.getElementById('cell-start').value=resolvedStart;
  document.getElementById('cell-end').value=resolvedEnd;
  // fill shift type — try exact match in dropdown first, else set custom
  const shiftSel=document.getElementById('cell-shifttype');
  const shiftCustom=document.getElementById('cell-shifttype-custom');
  let shiftMatched=false;
  for(let o of shiftSel.options){if(o.value===resolvedShift){shiftSel.value=resolvedShift;shiftMatched=true;break;}}
  if(!shiftMatched&&resolvedShift){
    shiftSel.value='__custom__';
    shiftCustom.style.display='block';
    shiftCustom.value=resolvedShift;
  } else {
    shiftCustom.style.display='none';
    shiftCustom.value='';
    if(!shiftMatched) shiftSel.value='';
  }
  // fill leave/book-off code
  document.getElementById('cell-code').value=resolvedBookoff;
  // fill cover/replacement name
  const nameSelect=document.getElementById('cell-empname');
  const nameCustomInput=document.getElementById('cell-empname-custom');
  let nameMatched=false;
  for(let o of nameSelect.options){
    if(o.value&&o.value!=='__agency__'&&(o.text===resolvedCover||o.value===resolvedCover)){
      nameSelect.value=o.value; nameMatched=true; break;
    }
  }
  if(!nameMatched&&resolvedCover){
    nameSelect.value='__agency__';
    nameCustomInput.style.display='block';
    nameCustomInput.value=resolvedCover.replace('*','')+(resolvedCover.includes('*')?'*':'');
  } else {
    nameCustomInput.style.display='none';
    nameCustomInput.value='';
    if(!nameMatched) nameSelect.value='';
  }
  openModal('cell-edit-modal');
}
/* saveCellEdit — see improved version below */

/* ===================== AVAILABILITY AMENDMENTS ===================== */
let availAmendData=[
  {emp:'Keon Pompey',type:'PT/Recall',submitted:'Mon Jun 16',effective:'Thu Jun 26',old:'Mon/Tue/Wed available',new:'Tue/Wed/Thu available',seen:{emp:false,mgmt:false,sched:false}},
];
function renderAvailAmends(){
  const el=document.getElementById('avail-amend-list');
  if(!el) return;
  if(!availAmendData.length){el.innerHTML='<p style="color:var(--t3);font-size:13px">No amendments on record.</p>';return;}
  el.innerHTML=availAmendData.map(a=>`
    <div class="card" style="border-left:3px solid var(--amber)">
      <div class="card-title">${a.emp} — Availability amendment</div>
      <table class="bt" style="font-size:12px"><tbody>
        <tr><td>Submitted</td><td>${a.submitted}</td></tr>
        <tr><td>Takes effect</td><td><b style="color:var(--amber)">${a.effective}</b></td></tr>
        <tr><td>Previous availability</td><td style="color:#c0392b"><s>${a.old}</s></td></tr>
        <tr><td>New availability</td><td style="color:var(--green)"><b>→ ${a.new}</b></td></tr>
        <tr><td>Acknowledged by</td><td>
          Employee: ${a.seen.emp?'✓':'⏳'} &nbsp; Scheduler: ${a.seen.sched?'✓':'⏳'} &nbsp; Management: ${a.seen.mgmt?'✓':'⏳'}
        </td></tr>
      </tbody></table>
    </div>`).join('');
}

/* ===================== UNIT RENAMING ===================== */
let unitNames={boys:'Boys',girls:'Girls'};
function renameUnit(unit){
  const current=unitNames[unit];
  const name=prompt('Rename "'+current+' Unit" to:',current);
  if(name&&name.trim()){
    unitNames[unit]=name.trim();
    notify('Unit renamed to "'+name.trim()+' Unit". Reflected in schedules and rosters.');
  }
}
function removeSchedule(){
  const name=prompt('Enter the schedule name to remove (type exactly):','');
  if(name&&name.trim()){
    if(confirm('Remove schedule "'+name.trim()+'"? This cannot be undone.')){
      notify('Schedule "'+name.trim()+'" removed.');
    }
  }
}

/* ===================== SCHEDULE TAB (Ed vs IA) ===================== */
function schedTab(unit,btn){
  ['ia','ed'].forEach(u=>{
    document.getElementById('sched-panel-'+u).style.display='none';
    const b=document.getElementById('sched-tab-'+u);
    if(b){b.style.background='';b.style.color='';b.style.borderColor='';}
  });
  document.getElementById('sched-panel-'+unit).style.display='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  document.getElementById('full-grid-area').innerHTML='';
}

/* ===================== EMPLOYEE MESSAGING ===================== */
let empMsgInbox=[
  {from:'Scheduling Admin',subject:'Schedule updated — PP 08',body:'The PP 08 schedule has been pushed. Please review your updated shifts under "My schedule".',ts:'Mon Jun 23',read:false},
  {from:'Greg Page',subject:'Shift switch offer',body:'Hey Keith — would you be open to switching your Mon Jun 23 J1 for my Wed Jun 25 J1? Let me know!',ts:'Sun Jun 22',read:true},
  {from:'Unit Manager',subject:'Reminder: Availability deadline',body:'Just a reminder that availability sheets for PP 09 are due by Wed Jun 25 at 9:00 AM.',ts:'Fri Jun 20',read:true},
];
let empMsgSent=[];
function empMsgTab(panel,btn){
  ['inbox','compose','sent'].forEach(p=>{
    document.getElementById('emsg-panel-'+p).style.display='none';
    const b=document.getElementById('emsg-tab-'+p);
    if(b){b.style.background='';b.style.color='';b.style.borderColor='';}
  });
  document.getElementById('emsg-panel-'+panel).style.display='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
  if(panel==='inbox') renderEmpInbox();
  if(panel==='sent') renderEmpSent();
}
function renderEmpInbox(){
  const el=document.getElementById('emp-inbox-list');
  if(!empMsgInbox.length){el.innerHTML='<p style="color:var(--t3);font-size:13px">No messages.</p>';return;}
  el.innerHTML=empMsgInbox.map((m,i)=>`
    <div style="background:${m.read?'var(--bg2)':'var(--bluelight)'};border:1px solid ${m.read?'var(--bd2)':'#85B7EB'};border-radius:var(--r);padding:10px 14px;margin-bottom:6px;font-size:12px;cursor:pointer" onclick="readEmpMsg(${i})">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <span style="font-weight:600">${m.from}</span>
        <span style="font-size:10px;color:var(--t3)">${m.ts}</span>
      </div>
      <div style="${m.read?'color:var(--t2)':'font-weight:600'}">${m.subject}</div>
      <div style="color:var(--t3);font-size:11px;margin-top:2px">${m.body.substring(0,80)}…</div>
    </div>`).join('');
}
function readEmpMsg(i){
  empMsgInbox[i].read=true;
  const m=empMsgInbox[i];
  const el=document.getElementById('emp-inbox-list');
  el.innerHTML=`<button class="btn" onclick="renderEmpInbox()" style="margin-bottom:.6rem">← Back to inbox</button>
    <div class="card">
      <div class="card-title">${m.subject}</div>
      <div style="font-size:11px;color:var(--t3);margin-bottom:.6rem">From: <b>${m.from}</b> · ${m.ts}</div>
      <div style="font-size:12px;line-height:1.6">${m.body}</div>
    </div>`;
}
function renderEmpSent(){
  const el=document.getElementById('emp-sent-list');
  if(!empMsgSent.length){el.innerHTML='<p style="color:var(--t3);font-size:13px">No sent messages yet.</p>';return;}
  el.innerHTML=empMsgSent.map(m=>`
    <div class="card" style="font-size:12px">
      <div style="display:flex;justify-content:space-between"><span>To: <b>${m.to}</b></span><span style="color:var(--t3);font-size:10px">${m.ts}</span></div>
      <div style="font-weight:600">${m.subject}</div>
      <div style="color:var(--t2);margin-top:4px">${m.body}</div>
    </div>`).join('');
}
function sendEmpMsg(){
  const to=document.getElementById('emp-msg-to').value;
  const subject=document.getElementById('emp-msg-subject').value||'General message';
  const body=document.getElementById('emp-msg-body').value.trim();
  if(!to||!body){alert('Please select a recipient and write a message.');return;}
  empMsgSent.unshift({to,subject,body,ts:'Now'});
  document.getElementById('emp-msg-body').value='';
  empMsgTab('sent',document.getElementById('emsg-tab-sent'));
  notify('Message sent to '+to+'.');
}

/* ===================== SHIFT SWITCH ===================== */
let switchRequests=[
  {from:'Greg Page',myShift:'Wed Jun 25 · J1 Day · Boys IA',theirShift:'Sat Jun 28 · S1 Eve · Boys IA',note:"My daughter's graduation is that evening.",status:'pending_me',ts:'Jun 20 9:41 AM'},
];
function switchTab(panel,btn){
  ['request','received','history'].forEach(p=>{
    document.getElementById('sw-panel-'+p).style.display='none';
    const b=document.getElementById('sw-tab-'+p);
    if(b){b.style.background='';b.style.color='';b.style.borderColor='';}
  });
  document.getElementById('sw-panel-'+panel).style.display='';
  btn.style.background='var(--bluelight)';btn.style.color='var(--blue)';btn.style.borderColor='#85B7EB';
}
function submitSwitchReq(){
  const sel=document.getElementById('sw-my-shift');
  const myShift=sel.options[sel.selectedIndex].text;
  const colleague=document.getElementById('sw-colleague').value;
  const want=document.getElementById('sw-want-shift').value.trim();
  const note=document.getElementById('sw-note').value.trim();
  notify('Switch request sent to '+colleague+'. You will be notified when they respond.');
  document.getElementById('sw-note').value='';
}
function respondSwitch(resp){
  if(resp==='accepted'){
    notify('Switch accepted — sent to management for approval. You and Greg Page will be notified of the decision.');
    document.getElementById('sw-panel-received').innerHTML='<p style="color:var(--t3);font-size:13px">No pending switch offers.</p>';
  } else {
    notify('Switch offer from Greg Page declined. They have been notified.');
    document.getElementById('sw-panel-received').innerHTML='<p style="color:var(--t3);font-size:13px">No pending switch offers.</p>';
  }
}

/* helper: show/hide custom name input when "Agency" is selected */
function cellNameSelectChange(sel){
  const customInput=document.getElementById('cell-empname-custom');
  if(sel.value==='__agency__'){
    customInput.style.display='block';
    customInput.focus();
  } else {
    customInput.style.display='none';
    customInput.value='';
  }
}

/* ===================== IMPROVED saveCellEdit (uses cellOverrides) ===================== */
/* show/hide custom shift text input when "Other — type below" chosen */
function cellShiftTypeChange(sel){
  const customInput=document.getElementById('cell-shifttype-custom');
  if(sel.value==='__custom__'){
    customInput.style.display='block';
    customInput.focus();
  } else {
    customInput.style.display='none';
    customInput.value='';
  }
}

/* remove the shift from a cell entirely — wipes override, resets to empty */
function removeCellShift(){
  if(!activeCellEl) return;
  const si=activeCellEl.dataset&&activeCellEl.dataset.si;
  const idx=activeCellEl.dataset&&activeCellEl.dataset.idx;
  if(si!==undefined&&idx!==undefined){
    delete cellOverrides[si+'-'+idx];
  }
  activeCellEl.className='cell em';
  activeCellEl.innerHTML='<span style="font-size:14px;color:rgba(0,0,0,.18);line-height:1">+</span>';
  activeCellEl.style.outline='';
  closeModal('cell-edit-modal');
  notify('Shift removed from cell.');
}

function saveCellEdit(){
  if(!activeCellEl){closeModal('cell-edit-modal');return;}
  const start=document.getElementById('cell-start').value;
  const end=document.getElementById('cell-end').value;
  // resolve shift type: dropdown OR custom text field
  let shiftType=document.getElementById('cell-shifttype').value.trim();
  if(shiftType==='__custom__'){
    shiftType=document.getElementById('cell-shifttype-custom').value.trim();
  }
  const nameSelect=document.getElementById('cell-empname').value;
  const nameCustom=document.getElementById('cell-empname-custom').value.trim();
  // resolve name: if agency selected, use typed custom name (add * if not present)
  let name='';
  if(nameSelect==='__agency__'){
    name=nameCustom?(nameCustom.includes('*')?nameCustom:nameCustom+'*'):'Agency*';
  } else {
    name=nameSelect.trim();
  }
  const bookoff=document.getElementById('cell-code').value.trim();
  const si=activeCellEl.dataset&&activeCellEl.dataset.si;
  const idx=activeCellEl.dataset&&activeCellEl.dataset.idx;
  // existing cell shift code (for display when no new shift chosen)
  const existingMainEl=activeCellEl.querySelector('.cell-main');
  const existingCode=existingMainEl?existingMainEl.textContent.trim():'';
  const displayCode=shiftType||existingCode||'—';
  if(si!==undefined&&idx!==undefined){
    cellOverrides[si+'-'+idx]={start,end,name,bookoff,shift:shiftType};
  }
  // rebuild visual to match buildGrid style — bookoff INLINE with shift code
  const isAgency=name.includes('*');
  const nameDisplay=name.replace('*','');
  const agencyStar=isAgency?'<span style="color:#f59e0b;font-weight:900">*</span>':'';
  let topLine='<div style="display:flex;align-items:center;gap:2px;flex-wrap:wrap;justify-content:center;line-height:1.2">'
    +'<span class="cell-main">'+displayCode+'</span>';
  if(bookoff) topLine+='<span style="background:#c0392b;color:#fff;border-radius:2px;font-size:7px;font-weight:800;padding:0 3px;letter-spacing:.3px">'+bookoff+'</span>';
  topLine+='</div>';
  let interior=topLine;
  if(name) interior+='<span style="color:#fff;background:rgba(0,0,0,.28);border-radius:2px;font-size:8px;font-weight:700;padding:1px 3px;display:block;margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:70px">▶ '+nameDisplay+agencyStar+'</span>';
  if(start&&end) interior+='<span style="font-size:8px;color:rgba(255,255,255,.8);font-weight:600;display:block;margin-top:1px">⏱ '+start+'–'+end+'</span>';
  // update cell colour class if shift type changed
  const classBase=shiftType||existingCode;
  if(classBase&&classBase!=='—'){
    activeCellEl.className='cell '+cellClass(classBase);
  }
  activeCellEl.innerHTML=interior;
  activeCellEl.style.outline='2px solid var(--amber)';
  closeModal('cell-edit-modal');
  notify('Cell updated. Employees see this at the next Mon/Wed/Fri push.');
}

/* ===================== TRAN/ESC MODAL FUNCTIONS ===================== */
function tranEscStaffChange(sel){
  const c=document.getElementById('tranesc-staff-custom');
  c.style.display=sel.value==='__agency__'?'block':'none';
  if(sel.value!=='__agency__') c.value='';
}
function openAddTranEsc(wi){
  document.getElementById('tranesc-edit-idx').value='-1';
  document.getElementById('tranesc-edit-pp').value=wi;
  document.getElementById('tranesc-modal-title').childNodes[0].textContent='Add Transport / Escort — Week '+(wi+1)+' ';
  document.getElementById('tranesc-type').value='TRAN';
  document.getElementById('tranesc-staff').value='';
  document.getElementById('tranesc-staff-custom').style.display='none';
  document.getElementById('tranesc-staff-custom').value='';
  document.getElementById('tranesc-start').value='';
  document.getElementById('tranesc-end').value='';
  document.getElementById('tranesc-day').value='0';
  document.getElementById('tranesc-note').value='';
  document.getElementById('tranesc-delete-btn').style.display='none';
  openModal('tranesc-modal');
}
function openAddTranEscDay(wi,day){
  openAddTranEsc(wi);
  document.getElementById('tranesc-day').value=String(day);
}
function openEditTranEsc(idx){
  const r=tranEscRows[idx];
  if(!r) return;
  document.getElementById('tranesc-edit-idx').value=String(idx);
  document.getElementById('tranesc-edit-pp').value=String(r.pp);
  document.getElementById('tranesc-modal-title').childNodes[0].textContent='Edit '+r.type+' entry ';
  document.getElementById('tranesc-type').value=r.type;
  // try to match staff name in select
  const sel=document.getElementById('tranesc-staff');
  let matched=false;
  for(let o of sel.options){ if(o.text===r.staff||o.value===r.staff){sel.value=o.value;matched=true;break;} }
  if(!matched){ sel.value='__agency__'; document.getElementById('tranesc-staff-custom').style.display='block'; document.getElementById('tranesc-staff-custom').value=r.staff; }
  else { document.getElementById('tranesc-staff-custom').style.display='none'; }
  document.getElementById('tranesc-start').value=r.start||'';
  document.getElementById('tranesc-end').value=r.end||'';
  document.getElementById('tranesc-day').value=String(r.day);
  document.getElementById('tranesc-note').value=r.note||'';
  document.getElementById('tranesc-delete-btn').style.display='inline-block';
  openModal('tranesc-modal');
}
function saveTranEsc(){
  const idx=parseInt(document.getElementById('tranesc-edit-idx').value);
  const pp=parseInt(document.getElementById('tranesc-edit-pp').value);
  const type=document.getElementById('tranesc-type').value;
  const staffSel=document.getElementById('tranesc-staff').value;
  const staffCustom=document.getElementById('tranesc-staff-custom').value.trim();
  const staff=staffSel==='__agency__'?(staffCustom||'Agency'):staffSel;
  const startRaw=document.getElementById('tranesc-start').value;
  // convert HH:MM to display
  const startDisplay=startRaw?startRaw:'—';
  const end=document.getElementById('tranesc-end').value||'—';
  const day=parseInt(document.getElementById('tranesc-day').value);
  const note=document.getElementById('tranesc-note').value.trim();
  const entry={pp,day,type,staff,start:startDisplay,end,note};
  if(idx>=0){ tranEscRows[idx]=entry; } else { tranEscRows.push(entry); }
  closeModal('tranesc-modal');
  // rebuild current grid
  if(currentGridStaff!==null){ buildGrid('mgmt-full-grid',true,currentGridStaff); }
  notify(type+' entry saved for '+(staff||'staff')+'. Grid updated.');
}
function deleteTranEsc(){
  const idx=parseInt(document.getElementById('tranesc-edit-idx').value);
  if(idx>=0) tranEscRows.splice(idx,1);
  closeModal('tranesc-modal');
  if(currentGridStaff!==null){ buildGrid('mgmt-full-grid',true,currentGridStaff); }
  notify('TRAN/ESC entry removed.');
}

/* ===================== HOOK NEW PAGES INTO page() and empPage() ===================== */
const _origPage=page;
page=function(id,el){
  _origPage(id,el);
  if(id==='empprofile'){renderEmpProfileList();}
  if(id==='loanservice'){renderLoanList();}
  if(id==='regularcontact'){renderRegContact();}
  if(id==='dropshiftmgmt'){renderDropMgmt();}
  if(id==='seniority'){senTab(currentSenUnit,document.getElementById(currentSenUnit==='educators'?'sen-tab-ed':'sen-tab-ia'));}
};
const _origEmpPage=empPage;
empPage=function(id,el){
  _origEmpPage(id,el);
  if(id==='emp-dropshift'){checkDropCode();}
  if(id==='emp-notifications'){renderNotifInbox();}
  if(id==='emp-messaging'){empMsgTab('inbox',document.getElementById('emsg-tab-inbox'));}
  if(id==='emp-switchshift'){switchTab('request',document.getElementById('sw-tab-request'));}
};
const _origPage2=page;
page=function(id,el){
  _origPage2(id,el);
  if(id==='schedules'){schedTab('ia',document.getElementById('sched-tab-ia'));}
};
</script>
</body>
</html>
