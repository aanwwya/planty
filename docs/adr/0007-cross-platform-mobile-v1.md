---
status: accepted
---

# v1 is a cross-platform mobile app

Rootly v1 is built with React Native and Expo for iOS and Android from one codebase.

The core interactions are native-feeling: camera capture, location permission, map browsing, and push reminders. One codebase keeps an agent-built v1 tractable and avoids maintaining two native apps before the product is validated. The cost is dependence on Expo's native module ecosystem and app-store release processes; features that require unusually deep native work may need custom modules later.
