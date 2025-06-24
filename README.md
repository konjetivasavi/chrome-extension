Company : CODETECH IT SOLUTIONS

Name : Konjeti Vasavi

INTERN ID : CT04DF720

Duration : 4-WEEKS

Mentor : Neela Santhosh Kumar

Description: To Develop A Chrome Extension For Time Tracking And Productivity Analytics

This Chrome extension is a **simple time tracker** that records how long you spend on different websites and then displays that data in a neat popup report. Its goal is to help you monitor your productivity by capturing the time spent on each domain.

The **core functionality** is split into two parts: a background service worker and a popup interface. The `background.js` file contains all the logic for tracking time. When you switch between tabs or navigate to a new page, the `chrome.tabs.onActivated` and `chrome.tabs.onUpdated` event listeners detect the change. Every time one of these events happens, the `switchSite()` function is triggered.

The `switchSite()` function is the heart of this tracker. It takes the current tab’s URL and extracts its hostname so that we can uniquely identify each site. If there was a previously active site, the code calculates the amount of time spent on it as the difference between the current time (`Date.now()`) and a `startTime` variable that was saved when the site was last visited. It then uses the `chrome.storage.local` API to store this accumulated time against the previous domain as a key-value pair. Essentially, this lets you build up a persistent record of all the minutes you spend browsing different websites over time.

Once the time for the old site is saved, the tracker updates its `currentSite` and `startTime` variables with the new hostname and a new timestamp. This way, every time you switch tabs or navigate to a new page, the timer resets for the new site.

The **popup interface** (as shown in the `popup.html` file) is a simple HTML page with a bit of inline CSS to make it look clean. It contains a `<ul>` list that will be populated with each tracked site. The popup’s embedded `<script>` runs when you click the extension icon. It calls `chrome.storage.local.get(null, ...)`, which returns all saved data for all domains. The script iterates through this data, converts the time from milliseconds into minutes (`(data[site] / 60000).toFixed(2)`), and dynamically constructs list items (`<li>`) that display each site’s hostname alongside its total tracked minutes.

The `manifest.json` file, set to version 3, ties everything together. It declares that the extension needs the `tabs` and `storage` permissions so it can read the active tab and save data. It also specifies that the background logic should run as a `service_worker` (`background.js`) and that `popup.html` is the action popup that will show up when you click the extension icon.

Altogether, this structure is lightweight and efficient. The `background.js` file silently tracks your browsing in the background without disturbing your workflow. The `popup.html` provides a quick dashboard so you can see your personal productivity report at any time. This is a practical, self-contained time-tracking extension that can easily be expanded — for example, by classifying sites as “productive” or “unproductive,” or by adding weekly or daily summaries — making it a perfect base for further productivity analytics.

Output:

Tracked Time (Minutes)

google.com → 8.50 mins  
youtube.com → 17.20 mins  
chat.openai.com → 5.33 mins  
linkedin.com → 3.25 mins
