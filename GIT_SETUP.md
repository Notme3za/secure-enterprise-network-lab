# Git publishing steps

Put the README, saved Packet Tracer `.pkt` file, and safe-to-share screenshots in one project folder.

Suggested layout:

secure-enterprise-network-lab/
├── README.md
├── GIT_SETUP.md
├── .gitignore
├── packet-tracer/
│   └── secure-enterprise-network-lab.pkt
└── screenshots/

From a terminal opened in that folder:

```bash
git init
git add README.md GIT_SETUP.md .gitignore packet-tracer screenshots
git status
git commit -m "Add secure enterprise network lab"