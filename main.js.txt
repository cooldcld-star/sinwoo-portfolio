const toast = document.getElementById("toast");

function showToast(msg) {
  toast.textContent = msg;
  toast.classList.add("show");
  clearTimeout(showToast._t);
  showToast._t = setTimeout(() => toast.classList.remove("show"), 1400);
}

async function copyText(text) {
  try {
    await navigator.clipboard.writeText(text);
    showToast("복사 완료!");
  } catch (e) {
    // fallback
    const ta = document.createElement("textarea");
    ta.value = text;
    document.body.appendChild(ta);
    ta.select();
    document.execCommand("copy");
    ta.remove();
    showToast("복사 완료!");
  }
}

document.getElementById("year").textContent = new Date().getFullYear();

document.getElementById("copyLinkBtn").addEventListener("click", () => {
  copyText(window.location.href);
});

document.getElementById("copyEmailBtn").addEventListener("click", () => {
  const email = document.getElementById("emailText").textContent.trim();
  copyText(email);
});

document.querySelectorAll("[data-copy]").forEach((btn) => {
  btn.addEventListener("click", () => copyText(btn.getAttribute("data-copy")));
});
