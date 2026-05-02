<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>MPAC Membership Registration</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700;800;900&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    :root {
      --primary: #0033CC;
      --primary-dark: #002299;
      --pink: #C2185B;
      --amber: #FFA000;
      --bg-light: #f4f7fc;
      --card-bg: rgba(255,255,255,0.92);
      --text-dark: #1e293b;
      --shadow: 0 8px 20px rgba(0,0,0,0.05);
      --radius: 28px;
    }
    body { font-family: 'Inter', sans-serif; background: var(--bg-light); color: var(--text-dark); padding: 20px; }
    .container { max-width: 1200px; margin: 0 auto; }
    .premium-header { background: linear-gradient(135deg, var(--primary-dark), #001166); border-radius: var(--radius); padding: 16px 28px; margin-bottom: 24px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; box-shadow: var(--shadow); color: white; }
    .logo-section { display: flex; align-items: center; gap: 16px; }
    .logo-badge { width: 54px; height: 54px; background: linear-gradient(135deg, var(--amber), var(--primary)); border-radius: 50%; display: flex; align-items: center; justify-content: center; overflow: hidden; box-shadow: 0 0 0 2px rgba(255,160,0,0.5); }
    .logo-badge img { width: 100%; height: 100%; object-fit: cover; }
    .header-text h1 { font-size: 1.5rem; font-weight: 800; }
    .light-motto { font-size: 0.75rem; opacity: 0.85; margin-top: 4px; color: #FFE0A3; }
    .stats-badge { display: flex; gap: 20px; background: rgba(0,0,0,0.3); padding: 6px 18px; border-radius: 60px; font-size: 0.8rem; }
    .stats-badge span { font-weight: 800; color: var(--amber); margin-left: 4px; }
    .sync-status { font-size: 0.7rem; background: rgba(0,0,0,0.4); padding: 2px 10px; border-radius: 40px; }
    .sync-status.offline { background: #C2185B; }
    .glass-card { background: var(--card-bg); border-radius: 32px; border: 1px solid rgba(0,0,0,0.06); margin-bottom: 24px; overflow: hidden; box-shadow: var(--shadow); }
    .card-header { padding: 16px 24px; background: rgba(0,0,0,0.02); border-bottom: 2px solid var(--amber); display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
    .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(360px, 1fr)); gap: 24px; padding: 28px; }
    .form-section { background: #f8fafc; border-radius: 24px; padding: 20px; border-left: 4px solid var(--primary); }
    .input-group { margin-bottom: 16px; }
    .input-group label { display: block; font-size: 0.7rem; font-weight: 700; text-transform: uppercase; color: var(--primary); margin-bottom: 6px; }
    .input-group input, .input-group select, .input-group textarea { width: 100%; padding: 10px 14px; background: white; border: 1px solid #e2e8f0; border-radius: 18px; font-family: inherit; }
    .radio-group { display: flex; gap: 24px; align-items: center; margin-top: 6px; flex-wrap: wrap; }
    .phone-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; }
    .btn-gold { background: linear-gradient(95deg, var(--primary), var(--primary-dark)); border: none; padding: 14px; border-radius: 60px; font-weight: 800; color: white; cursor: pointer; width: 100%; transition: 0.2s; }
    .btn-gold:disabled { opacity: 0.6; cursor: not-allowed; }
    .btn-outline { background: rgba(0,51,204,0.08); border: 1px solid var(--pink); padding: 8px 18px; border-radius: 60px; cursor: pointer; font-weight: 600; transition: 0.2s; }
    .btn-outline:hover { background: var(--pink); color: white; border-color: var(--pink); }
    .checkbox-label { display: flex; align-items: center; gap: 12px; margin: 16px 0 12px; }
    .inline-note { font-size: 0.7rem; color: #64748b; margin-top: 8px; }
    .toast { position: fixed; bottom: 20px; right: 20px; background: var(--primary-dark); color: white; padding: 10px 20px; border-radius: 40px; display: none; z-index: 2100; font-weight: bold; box-shadow: var(--shadow); }
    @media (max-width: 800px) { .phone-row { grid-template-columns: 1fr; } .form-grid { padding: 16px; } }
  </style>
</head>
<body>
<div class="container">
  <div class="premium-header">
    <div class="logo-section">
      <div class="logo-badge"><img src="https://i.imgur.com/kTumLOY.jpg" alt="MPAC Logo" onerror="this.src='https://via.placeholder.com/54?text=MPAC'"></div>
      <div class="header-text">
        <h1>MPAC Membership Hub</h1>
        <div class="light-motto"><i class="fas fa-cloud-upload-alt"></i> Live Google Sheets Sync</div>
      </div>
    </div>
    <div style="display: flex; gap: 15px; align-items: center;">
      <div class="stats-badge"><i class="fas fa-users"></i> <span id="totalMembersCount">0</span> Members</div>
      <div class="sync-status" id="syncStatus"><i class="fas fa-circle"></i> Live</div>
    </div>
  </div>

  <!-- REGISTRATION ONLY – no tabs -->
  <div class="glass-card">
    <div class="card-header"><h3><i class="fas fa-pen-ruler"></i> Member Registration Form</h3><button class="btn-outline" id="resetFormBtn"><i class="fas fa-undo-alt"></i> Clear Form</button></div>
    <form id="memberForm">
      <div class="form-grid">
        <div class="form-section">
          <h4><i class="fas fa-user-circle" style="color:var(--primary);"></i> Personal Information</h4>
          <div class="input-group"><label>Full Name & Surname *</label><input type="text" id="fullName" required></div>
          <div class="input-group"><label>Date of Birth *</label><input type="date" id="dob" required></div>
          <div class="input-group"><label>Marital Status</label><select id="maritalStatus"><option>Married</option><option>Single</option><option>Widowed</option><option>Separated</option></select></div>
          <div class="input-group"><label>Place of Birth</label><input type="text" id="placeOfBirth"></div>
          <div class="input-group"><label>ID Number *</label><input type="text" id="idNumber" required></div>
          <div class="input-group"><label>Postal Address</label><input type="text" id="postalAddress"></div>
          <div class="input-group"><label>Physical Address</label><input type="text" id="physicalAddress"></div>
          <div class="phone-row"><div class="input-group"><label>Home</label><input type="tel" id="phoneHome"></div><div class="input-group"><label>Work</label><input type="tel" id="phoneWork"></div><div class="input-group"><label>Cell *</label><input type="tel" id="phoneCell" required></div></div>
          <div class="input-group"><label>Email *</label><input type="email" id="email" required></div>
          <div class="input-group"><label>Next of Kin</label><input type="text" id="nextOfKin"></div>
          <div class="input-group"><label>Children count</label><input type="number" id="childrenCount" min="0" value="0"></div>
        </div>
        <div class="form-section">
          <h4><i class="fas fa-church" style="color:var(--pink);"></i> Spiritual Information</h4>
          <div class="input-group"><label>Member of any Christian denomination?</label><div class="radio-group"><label><input type="radio" name="denomMember" value="yes"> Yes</label><label><input type="radio" name="denomMember" value="no" checked> No</label></div></div>
          <div id="associateChurchGroup" style="display:none;"><div class="input-group"><label>Associate Church/Ministry</label><input type="text" id="associateChurchName"></div></div>
          <div id="pastorGroup" style="display:none;"><div class="input-group"><label>Pastor’s details</label><textarea id="pastorDetails" rows="2"></textarea></div></div>
          <div class="input-group"><label>Born again?</label><div class="radio-group"><label><input type="radio" name="bornAgain" value="yes"> Yes</label><label><input type="radio" name="bornAgain" value="no" checked> No</label></div></div>
          <div id="bornAgainYearGroup" style="display:none;"><div class="input-group"><label>Year born again</label><input type="text" id="bornAgainYear"></div></div>
          <div class="input-group"><label>What would you like to do in Church?</label><input type="text" id="churchDesire"></div>
          <div class="input-group"><label>Current involvement</label><textarea id="churchInvolvement" rows="2"></textarea></div>
          <div class="input-group"><label>Water baptism?</label><div class="radio-group"><label><input type="radio" name="baptised" value="yes"> Yes</label><label><input type="radio" name="baptised" value="no"> No</label></div></div>
        </div>
        <div class="form-section">
          <h4><i class="fas fa-file-signature" style="color:var(--amber);"></i> Declaration & Commitment</h4>
          <div class="input-group"><label>I, (full name) declare truth *</label><input type="text" id="declarationName" required></div>
          <div class="input-group"><label>Declaration Date</label><input type="date" id="declarationDate" required></div>
          <div class="checkbox-label"><input type="checkbox" id="commitmentCheckbox"> <label>I submit to MPAC leadership & activities.</label></div>
          <div class="inline-note"><i class="fas fa-info-circle"></i> By submitting, you confirm all details are truthful.</div>
        </div>
      </div>
      <div style="padding:0 28px 28px">
        <button type="submit" class="btn-gold" id="submitBtn"><i class="fas fa-save"></i> Register Member</button>
        <div style="margin-top:12px"><button type="button" id="cancelEditBtn" class="btn-outline" style="display:none;"><i class="fas fa-times"></i> Cancel Edit</button></div>
      </div>
    </form>
  </div>
</div>
<div id="toast" class="toast"></div>

<script>
  // ========== 🔴 REPLACE THIS URL WITH YOUR DEPLOYED WEB APP URL 🔴 ==========
  const API_BASE = "https://script.google.com/macros/s/AKfycbzO0roUGXv_cozk1hHI-TsPZ5Oq7JWKSc0RXYK-lCava725nQyN_NBMdZBI20-9NH_p/exec";
  // =========================================================================

  let members = [];
  let editId = null;
  let isSaving = false;

  function showToast(msg, isErr = false) {
    const toast = document.getElementById('toast');
    toast.textContent = msg;
    toast.style.display = 'block';
    toast.style.background = isErr ? '#C2185B' : 'var(--primary-dark)';
    setTimeout(() => toast.style.display = 'none', 3000);
  }

  function setSyncStatus(online) {
    const statusDiv = document.getElementById('syncStatus');
    if (online) {
      statusDiv.innerHTML = '<i class="fas fa-circle"></i> Live';
      statusDiv.style.background = 'rgba(0,0,0,0.4)';
    } else {
      statusDiv.innerHTML = '<i class="fas fa-exclamation-triangle"></i> Offline (local)';
      statusDiv.style.background = '#C2185B';
    }
  }

  async function fetchMembers() {
    try {
      setSyncStatus(true);
      const res = await fetch(`${API_BASE}?action=list&_=${Date.now()}`);
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      const json = await res.json();
      if (json.status === 'success') {
        members = json.data || [];
        localStorage.setItem('mpac_members_backup', JSON.stringify(members));
        setSyncStatus(true);
      } else {
        throw new Error(json.error || 'Unknown error');
      }
    } catch (err) {
      console.warn('API fetch failed, loading from localStorage', err);
      setSyncStatus(false);
      const backup = localStorage.getItem('mpac_members_backup');
      members = backup ? JSON.parse(backup) : [];
      if (members.length) showToast('Using offline cache - sync will resume when online', true);
      else showToast('Unable to connect to server. Check script deployment.', true);
    }
    updateCounters();
  }

  async function addMember(data) {
    try {
      await fetch(API_BASE, {
        method: 'POST',
        mode: 'no-cors',
        body: JSON.stringify({ action: 'add', ...data }),
        headers: { 'Content-Type': 'application/json' }
      });
      return true;
    } catch (err) {
      console.warn('Add member error:', err);
      return false;
    }
  }

  async function updateMember(id, data) {
    try {
      await fetch(API_BASE, {
        method: 'POST',
        mode: 'no-cors',
        body: JSON.stringify({ action: 'update', id, ...data }),
        headers: { 'Content-Type': 'application/json' }
      });
      return true;
    } catch (err) {
      console.warn('Update member error:', err);
      return false;
    }
  }

  // (We keep deleteMember because it's used in edit mode, but no UI for it unless we add a delete button)
  // For simplicity, we can keep it but won't show a delete button. The edit mode still exists.
  async function deleteMember(id) {
    if (!confirm('⚠️ Permanently delete this member? This cannot be undone.')) return;
    try {
      await fetch(`${API_BASE}?action=delete&id=${id}`, { mode: 'no-cors' });
      await fetchMembers();
      showToast('Member deleted');
      if (editId === id) cancelEdit();
    } catch (err) {
      showToast('Error deleting - check connection', true);
    }
  }

  function editMember(id) {
    const m = members.find(x => x.id === id);
    if (!m) return;
    editId = id;
    document.getElementById('fullName').value = m.fullName || '';
    document.getElementById('dob').value = m.dob || '';
    document.getElementById('maritalStatus').value = m.maritalStatus || 'Married';
    document.getElementById('placeOfBirth').value = m.placeOfBirth || '';
    document.getElementById('idNumber').value = m.idNumber || '';
    document.getElementById('postalAddress').value = m.postalAddress || '';
    document.getElementById('physicalAddress').value = m.physicalAddress || '';
    document.getElementById('phoneHome').value = m.phoneHome || '';
    document.getElementById('phoneWork').value = m.phoneWork || '';
    document.getElementById('phoneCell').value = m.phoneCell || '';
    document.getElementById('email').value = m.email || '';
    document.getElementById('nextOfKin').value = m.nextOfKin || '';
    document.getElementById('childrenCount').value = m.childrenCount || 0;
    if (m.memberOfDenomination === 'yes') document.querySelector('input[name="denomMember"][value="yes"]').checked = true;
    else document.querySelector('input[name="denomMember"][value="no"]').checked = true;
    toggleDenominationFields();
    document.getElementById('associateChurchName').value = m.associateChurchName || '';
    document.getElementById('pastorDetails').value = m.pastorDetails || '';
    if (m.isBornAgain === 'yes') document.querySelector('input[name="bornAgain"][value="yes"]').checked = true;
    else document.querySelector('input[name="bornAgain"][value="no"]').checked = true;
    toggleBornAgainYear();
    document.getElementById('bornAgainYear').value = m.bornAgainYear || '';
    document.getElementById('churchDesire').value = m.churchDesire || '';
    document.getElementById('churchInvolvement').value = m.churchInvolvement || '';
    if (m.isBaptised === 'yes') document.querySelector('input[name="baptised"][value="yes"]').checked = true;
    else if (m.isBaptised === 'no') document.querySelector('input[name="baptised"][value="no"]').checked = true;
    document.getElementById('declarationName').value = m.declarationName || '';
    document.getElementById('declarationDate').value = m.declarationDate || '';
    document.getElementById('commitmentCheckbox').checked = m.commitmentAgreed === true;
    document.getElementById('submitBtn').innerHTML = '<i class="fas fa-edit"></i> Update Member';
    document.getElementById('cancelEditBtn').style.display = 'inline-block';
    showToast('✏️ Editing mode – make changes and click Update');
  }

  function cancelEdit() {
    editId = null;
    resetForm();
    document.getElementById('submitBtn').innerHTML = '<i class="fas fa-save"></i> Register Member';
    document.getElementById('cancelEditBtn').style.display = 'none';
  }

  function resetForm() {
    document.getElementById('memberForm').reset();
    document.getElementById('declarationDate').valueAsDate = new Date();
    document.getElementById('childrenCount').value = 0;
    document.querySelector('input[name="denomMember"][value="no"]').checked = true;
    toggleDenominationFields();
    document.querySelector('input[name="bornAgain"][value="no"]').checked = true;
    toggleBornAgainYear();
  }

  function getFormData() {
    const isDenom = document.querySelector('input[name="denomMember"]:checked').value === 'yes';
    return {
      fullName: document.getElementById('fullName').value.trim(),
      dob: document.getElementById('dob').value,
      maritalStatus: document.getElementById('maritalStatus').value,
      placeOfBirth: document.getElementById('placeOfBirth').value,
      idNumber: document.getElementById('idNumber').value.trim(),
      postalAddress: document.getElementById('postalAddress').value,
      physicalAddress: document.getElementById('physicalAddress').value,
      phoneHome: document.getElementById('phoneHome').value,
      phoneWork: document.getElementById('phoneWork').value,
      phoneCell: document.getElementById('phoneCell').value.trim(),
      email: document.getElementById('email').value.trim(),
      nextOfKin: document.getElementById('nextOfKin').value,
      childrenCount: parseInt(document.getElementById('childrenCount').value) || 0,
      memberOfDenomination: isDenom ? 'yes' : 'no',
      associateChurchName: isDenom ? document.getElementById('associateChurchName').value : '',
      pastorDetails: isDenom ? document.getElementById('pastorDetails').value : '',
      isBornAgain: document.querySelector('input[name="bornAgain"]:checked').value,
      bornAgainYear: document.getElementById('bornAgainYear').value,
      churchDesire: document.getElementById('churchDesire').value,
      churchInvolvement: document.getElementById('churchInvolvement').value,
      isBaptised: document.querySelector('input[name="baptised"]:checked')?.value || '',
      declarationName: document.getElementById('declarationName').value.trim(),
      declarationDate: document.getElementById('declarationDate').value,
      commitmentAgreed: document.getElementById('commitmentCheckbox').checked
    };
  }

  function validateFormData(data) {
    if (!data.fullName) { showToast('Full name is required', true); return false; }
    if (!data.idNumber) { showToast('ID Number is required', true); return false; }
    if (!data.phoneCell) { showToast('Cell phone number is required', true); return false; }
    if (!data.email || !data.email.includes('@')) { showToast('Valid email required', true); return false; }
    if (!data.dob) { showToast('Date of Birth required', true); return false; }
    if (!data.declarationName) { showToast('Declaration name required', true); return false; }
    if (!data.commitmentAgreed) { showToast('You must agree to the declaration', true); return false; }
    return true;
  }

  document.getElementById('memberForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    if (isSaving) return;
    const data = getFormData();
    if (!validateFormData(data)) return;

    const submitBtn = document.getElementById('submitBtn');
    const originalText = submitBtn.innerHTML;
    submitBtn.disabled = true;
    submitBtn.innerHTML = '<i class="fas fa-spinner fa-pulse"></i> Saving...';
    isSaving = true;

    try {
      let success = false;
      if (editId) success = await updateMember(editId, data);
      else success = await addMember(data);
      await fetchMembers();
      showToast(editId ? 'Member updated!' : 'Member registered!');
      if (editId) cancelEdit();
      else resetForm();
    } catch (err) {
      console.error(err);
      showToast('Network error. Please try again.', true);
    } finally {
      submitBtn.disabled = false;
      submitBtn.innerHTML = originalText;
      isSaving = false;
    }
  });

  function toggleDenominationFields() {
    const isMember = document.querySelector('input[name="denomMember"]:checked').value === 'yes';
    document.getElementById('associateChurchGroup').style.display = isMember ? 'block' : 'none';
    document.getElementById('pastorGroup').style.display = isMember ? 'block' : 'none';
    if (!isMember) {
      document.getElementById('pastorDetails').value = '';
      document.getElementById('associateChurchName').value = '';
    }
  }
  function toggleBornAgainYear() {
    const isBorn = document.querySelector('input[name="bornAgain"]:checked').value === 'yes';
    document.getElementById('bornAgainYearGroup').style.display = isBorn ? 'block' : 'none';
    if (!isBorn) document.getElementById('bornAgainYear').value = '';
  }

  document.querySelectorAll('input[name="denomMember"]').forEach(r => r.addEventListener('change', toggleDenominationFields));
  document.querySelectorAll('input[name="bornAgain"]').forEach(r => r.addEventListener('change', toggleBornAgainYear));

  document.getElementById('resetFormBtn')?.addEventListener('click', () => cancelEdit());
  document.getElementById('cancelEditBtn')?.addEventListener('click', cancelEdit);

  function updateCounters() { document.getElementById('totalMembersCount').innerText = members.length; }

  // Expose global functions for inline onclick (if we add edit/delete buttons in the future)
  window.editMember = editMember;
  window.deleteMember = deleteMember;

  toggleDenominationFields();
  toggleBornAgainYear();
  document.getElementById('declarationDate').valueAsDate = new Date();
  fetchMembers();
</script>
</body>
</html>
