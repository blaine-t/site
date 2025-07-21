+++
title = "LISA"
description = "LISA is an AI college advisor, and she's not just a chatbot: she has a voice and a face, and you talk to her over a video call!"
weight = 2

[extra]
local_image = "img/projects/lisa.avif"
local_image_webp = "img/projects/lisa.webp"
local_image_png = "img/projects/lisa.png"
+++

We built LISA, an AI assistant whose name stands for "Local Intelligent School Advisor". She's an AI college advisor, and she's not just a chatbot: she has a voice and a face, and you talk to her over a video call! Using Red Hat's OpenShift AI platform, user speech is transcribed into text and fed into a large language model that utilizes Intel AMX hardware acceleration. The response is then converted back into audio and spoken in an animation by LISA herself. Her language model is trained on the courses provided at your university, giving you immediate responses and information about what courses you need to take. Conveniently, the OpenShift platform provided all the AI components we needed to take a user’s speech audio, convert it to text, and prompt a custom LLM for LISA’s response.

We built this project in 24 hours at Hack Midwest 2024, and it received 2nd place for the Red Hat & Intel OpenShift AI Challenge. See below for a description of what LISA does. We deployed the app on the OpenShift platform during the competition, and the code in this repo is completely open-source. We aren't able to provide LISA's face model though since we modeled it after a real person at the hackathon (and it turned out somewhat creepy lol). If you are interested in taking this project further or spinning up your own instance of LISA, feel free to reach out to us and we can help out!



Source code and more information [available on Github](https://github.com/USS-Watson/lisa)!
