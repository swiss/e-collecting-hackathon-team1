# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## The GNU Privacy Handbook 
https://www.gnupg.org/gph/en/manual/book1.html

Das Starter-Handbuch von GnuPG — ist eine praxisorientierte Einführung, die erklärt, wie man mit GnuPG sichere Kommunikation durch Schlüsselerzeugung, Schlüsselaustausch, Verschlüsselung/Entschlüsselung und digitale Signaturen realisiert. 

The GNU Privacy Handbook is a practical beginner’s guide that explains how to use GnuPG for secure communication, including key generation, key exchange, encryption/decryption, and digital signatures.

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.


**Please help us to review the code below**

<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Mock GPG + SHA-512 (team1) — random number outside block</title>
<style>
  body { font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; padding: 28px; background:#f7fafc; color:#0f172a; }
  h1 { margin: 0 0 8px 0; font-size: 20px; }
  p { margin: 6px 0 14px 0; color:#334155 }
  .meta { display:flex; gap:12px; align-items:center; flex-wrap:wrap; margin-bottom:12px; }
  .label { color:#475569; font-size:13px; }
  .value { background:#fff; border:1px solid #e2e8f0; padding:8px 10px; border-radius:8px; font-family:monospace; }
  pre { background: #0b1220; color: #cbd5e1; padding: 16px; border-radius: 8px; overflow:auto; white-space:pre-wrap; word-break:break-word;}
  .controls { margin-top: 12px; display:flex; gap:8px; flex-wrap:wrap; }
  button { background:#0369a1; color:white; border:none; padding:8px 12px; border-radius:6px; cursor:pointer; }
  button.secondary { background:#94a3b8; color:#071233; }
  .note { margin-top:12px; font-size:13px; color:#475569; }
</style>
</head>
<body>
  <h1>Mock GPG Public Key + SHA-512 — author: <strong>team1</strong></h1>
  <p>Random number related to a signature is shown <strong>outside</strong> the mock GPG block. The file to download and to verify is named <code>&lt;random-number&gt;.asc</code>. it's SHA-512 is computed on the block content.</p>

  <div class="meta">
    <div class="label">Random number:</div>
    <div id="randNum" class="value">-</div>

    <div class="label">Filename:</div>
    <div id="filename" class="value">-</div>

    <div class="label">SHA-512:</div>
    <div id="sha512" class="value" style="min-width:420px">-</div>
  </div>

  <pre id="gpgBlock" aria-live="polite">Generating…</pre>

  <div class="controls">
    <button id="regenerate">Regenerate</button>
    <button id="copy" class="secondary">Copy GPG block</button>
    <button id="download" class="secondary">Download .asc</button>
    <button id="copySha" class="secondary">Copy SHA-512</button>
  </div>

  <div class="note">
    ⚠️ This is a mock PGP public key block for testing/display. It is <em>not</em> a real PGP public key and must not be used as one.
  </div>

<script>
/*
  mock-gpg-team1-rand-outside.html
  - Places random decimal number OUTSIDE the mock GPG block.
  - File name = <random-number>.asc
  - SHA-512 is computed for the block content (and shown).
  - Buttons: regenerate, copy block, download file, copy sha.
*/

function toHex(bytes) {
  return Array.from(bytes).map(b => b.toString(16).padStart(2, '0')).join('');
}

function randomHexString(lenBytes=8) {
  const arr = new Uint8Array(lenBytes);
  crypto.getRandomValues(arr);
  return toHex(arr);
}

function randomDecimalNumberString() {
  // create an 8-byte random number and convert to decimal string (compact but large)
  const arr = new Uint8Array(8);
  crypto.getRandomValues(arr);
  const hex = toHex(arr);
  const n = BigInt('0x' + hex);
  return n.toString(10);
}

function randomBase64Line(bytesCount) {
  const arr = new Uint8Array(bytesCount);
  crypto.getRandomValues(arr);
  let binary = '';
  for (let i = 0; i < arr.length; i++) binary += String.fromCharCode(arr[i]);
  return btoa(binary);
}

function buildMockGpgBlock() {
  // Build a mock PGP-like block. Note: NO random number line inside the block.
  const lines = [];
  for (let i=0;i<8;i++){
    lines.push(randomBase64Line(48));
  }
  const tail = randomHexString(4);

  const block = [
    "-----BEGIN PGP PUBLIC KEY BLOCK-----",
    "",
    "Version: Mock GPG v1.0",
    "",
    ...lines,
    "=",
    tail,
    "",
    "-----END PGP PUBLIC KEY BLOCK-----",
    "",
    "Author: team1"
  ];
  return block.join("\n");
}

async function sha512HexFromString(str) {
  const encoder = new TextEncoder();
  const data = encoder.encode(str);
  const hashBuffer = await crypto.subtle.digest('SHA-512', data);
  return toHex(new Uint8Array(hashBuffer));
}

async function generateAll() {
  // random number outside the block
  const randNum = randomDecimalNumberString();
  const filename = randNum + ".asc";
  const block = buildMockGpgBlock();
  const sha = await sha512HexFromString(block);

  // update DOM
  document.getElementById('randNum').textContent = randNum;
  document.getElementById('filename').textContent = filename;
  document.getElementById('sha512').textContent = sha;
  const pre = document.getElementById('gpgBlock');
  pre.textContent = block;

  // store for actions
  pre.dataset.content = block;
  pre.dataset.filename = filename;
  pre.dataset.sha512 = sha;
  pre.dataset.rand = randNum;
}

document.getElementById('regenerate').addEventListener('click', async () => {
  document.getElementById('gpgBlock').textContent = 'Regenerating…';
  await generateAll();
});

document.getElementById('copy').addEventListener('click', async () => {
  const pre = document.getElementById('gpgBlock');
  const text = pre.dataset.content || pre.textContent;
  try {
    await navigator.clipboard.writeText(text);
    alert('GPG block copied to clipboard');
  } catch (e) {
    alert('Copy failed: ' + e);
  }
});

document.getElementById('copySha').addEventListener('click', async () => {
  const sha = document.getElementById('gpgBlock').dataset.sha512 || document.getElementById('sha512').textContent;
  try {
    await navigator.clipboard.writeText(sha);
    alert('SHA-512 copied to clipboard');
  } catch (e) {
    alert('Copy failed: ' + e);
  }
});

document.getElementById('download').addEventListener('click', () => {
  const pre = document.getElementById('gpgBlock');
  const text = pre.dataset.content || pre.textContent;
  const filename = pre.dataset.filename || (Date.now() + ".asc");
  const blob = new Blob([text], {type: 'text/plain'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  document.body.appendChild(a);
  a.click();
  a.remove();
  URL.revokeObjectURL(url);
});

// Generate immediately on load
generateAll().catch(err => {
  console.error(err);
  document.getElementById('gpgBlock').textContent = "Error generating content: " + String(err);
});
</script>
</body>
</html>
<!--Thanks to openAi for the help-->


