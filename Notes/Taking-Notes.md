# OSCP Note-Taking Resources

[![My Shop](https://img.shields.io/badge/My%20Shop-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech/extras)
[![Medium](https://img.shields.io/badge/Medium-%40verylazytech-%231572B6?style=flat&logo=medium&logoColor=white)](https://medium.com/@verylazytech)
[![Github](https://img.shields.io/badge/Github-verylazytech-%23181717?style=flat&logo=github&logoColor=white)](https://github.com/verylazytech)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech)
[![My GitBook](https://img.shields.io/badge/My%20GitBook-VeryLazyTech-%23FFDD00?style=flat&logo=gitbook&logoColor=white)](https://www.verylazytech.com)
[![X](https://img.shields.io/twitter/url?url=https%3A%2F%2Fx.com%2Fverylazytech)](https://x.com/verylazytech)

## Tools for Note-Taking

- [CherryTree](https://www.giuspen.com/cherrytree/) - A hierarchical note-taking application with rich text and code support, perfect for OSCP.  
- [OffSec-Reporting](https://github.com/Syslifters/OffSec-Reporting) - Pentest Reporting made easy: Design in HTML, Write in Markdown, Render to PDF. Self-hosted or Cloud.


## Tutorials and Guides for OSCP Note-Taking

- [John Hammond](https://www.youtube.com/watch?v=MQGozZzHUwQ) - OSCP - Taking Notes & Resources.
- [Conda](https://www.youtube.com/watch?v=yYmDQY1zKKE) - OSCP - How to Take Effective Notes.
- [Elevate Cyber](https://www.youtube.com/watch?v=dX0IVDPo7ek) - My Top Note Taking Strategies for OSCP


## Tips for Effective Note-Taking

### Automate Saved shell output:
It only takes a single step to set up:
Copy-and-paste the following script to the end of ~/.zshrc.
```
if [ -z "${UNDER_SCRIPT}" ]; then
    logdir=${HOME}/logs
    logfile=${logdir}/$(date +%F.%H-%M-%S).$$.log

    mkdir -p ${logdir}
    export UNDER_SCRIPT=${logfile}
    echo "The terminal output is saving to $logfile"
    script -f -q ${logfile}

    exit
fi
```

That's it. Now every command's input and output will be recorded and saved in a safe place under ~/logs/ with a timestamp.
These changes will be effective in new windows/tabs.

Demo:
Whenever a new shell session is created, the log path of that session is displayed.

![image](https://github.com/user-attachments/assets/e8407b30-8007-47a3-92ef-058f41aa76c1)

View the logs by using cat.
It will show the log content including the colors of previous inputs and outputs.

![image](https://github.com/user-attachments/assets/aedc6063-8186-48d9-b78b-88020c9b8925)



