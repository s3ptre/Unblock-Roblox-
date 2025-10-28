copy this code

    let buttons = [...document.querySelectorAll('.user-blocking-btn')].filter(b => b.textContent.trim() === 'Unblock');
    let done = 0;
    let limit = 200; // change this to how many people you want to unblock but roblox might have a limit on how many you can unblock at once (50) so you need to refresh page and restart.

    async function unblockall() {
      for (let b of buttons) {
        if (done >= limit) break;

        let box = b.closest('.blocked-users-item');
        let nameBox = box?.querySelector('.blocked-user-name');
        let display = nameBox?.childNodes[0]?.textContent?.trim() || 'unknown';
        let handle = nameBox?.querySelector('.text-secondary')?.textContent?.trim() || '';

        b.click();
        await new Promise(r => setTimeout(r, 300));

        let confirm = [...document.querySelectorAll('.modal-footer button')]
          .find(x => x.textContent.trim() === 'Unblock');
        if (confirm) {
          confirm.click();
          done++;
          console.log(`Unblocked: ${display} (${handle}) — ${done}/${limit}`);
        } else {
          console.log(`Couldn't unblock : ${display} (${handle})`);
        }

        await new Promise(r => setTimeout(r, 0)); // delay
      }

      console.log(`FINISHED ! Unblocked ${done} users.`);
    }

    unblockall();
