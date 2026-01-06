# Free_Tweaks_Remove_BookMark_X

Automatically Close Modal Popup (#myModal)
This script automatically detects and closes a modal popup with the ID #myModal whenever it appears on the page. It is useful for dismissing repetitive or annoying prompts without user interaction.

✅ Features:
Automatically watches the page for the appearance of the modal.

Clicks the × (close) button as soon as the modal appears.

No need for manual intervention or repeated pasting.

🔧 How it works:
It uses a MutationObserver to monitor DOM changes. When a #myModal element becomes visible (i.e., display: block), it simulates a click on the close button.

---------------------- Code --------------------------------------


const observer = new MutationObserver(() => {
    const modal = document.getElementById("myModal");
    if (modal && modal.style.display === "block") {
        const closeButton = modal.querySelector("span");
        if (closeButton && closeButton.textContent.trim() === "×") {
            closeButton.click();
            console.log("Popup otomatik kapatıldı.");
        }
    }
});

observer.observe(document.body, { childList: true, subtree: true });



------------------------- New Code ----------------------------------------

(() => {
  console.log("Auto-clicker started");

  const clickedElements = new WeakSet();

  const clickElement = (el, label) => {
    if (clickedElements.has(el)) return;

    clickedElements.add(el);

    el.dispatchEvent(new MouseEvent("mousedown", { bubbles: true }));
    el.dispatchEvent(new MouseEvent("mouseup", { bubbles: true }));
    el.dispatchEvent(new MouseEvent("click", { bubbles: true }));

    console.log(`${label} clicked`);
  };

  const observer = new MutationObserver(() => {

    // 🔹 Upgrade popup button
    document.querySelectorAll("button").forEach(btn => {
      if (btn.textContent.trim() === "Upgrade") {
        clickElement(btn, "Upgrade");
      }
    });

    // 🔹 Remove All Bookmarks button
    document.querySelectorAll("button.ndy_twitter_bkmk_rm_btn").forEach(btn => {
      if (btn.textContent.trim() === "Remove All Bookmarks") {
        clickElement(btn, "Remove All Bookmarks");
      }
    });

  });

  observer.observe(document.body, {
    childList: true,
    subtree: true
  });

})();


------------------------------------------------------------------

Open the browser developer console (F12 > Console tab).

Paste the code above and hit Enter.

The script will now run in the background and auto-close any matching popup.



