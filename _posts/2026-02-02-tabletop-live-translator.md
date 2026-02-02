---
title: "Tabletop Live Translator"
layout: post_with_subscribe
category: projects
tags: [hardware, translation, raspberry-pi, gcp]
---

I have a friend from Ukraine. She primarily speaks Russian, though she knows a little English. I’ve learned a very small amount of Russian. I noticed that the process of taking a phone out of a pocket, opening Google Translate, talking into it, waiting for it to go ding, and holding the phone out to the other person involved just enough friction that we tended not to do it unless our hand gestures and nods were insufficient for a topic.

More convenient translators are coming quickly, but I didn’t have any in my hands yet. My Meta glasses can do it, but they don’t support Russian. Some AirPods can do it, but I didn’t have the right iPhone and she didn’t have the right AirPods. Probably the money spent on the hardware for this DIY solution could have gone toward upgrading that tech, but DIY is more fun, and you can build it to your exact preferences.

In this case, I wanted a face-to-face translation device on my kitchen counter or dining table. I wanted us to be able to walk up to it when we felt like having a conversation and just push a button to start.

---

## The ChatGPT Prompt


> *“hi. I'm gonna build a live translator. I want it to have two screens back to back, so people having a face to face conversation can use it. I want it to have two microphones, ideally with a push to talk button on the mic. when a person speaks into the English mic, it automatically and quickly transcribes what they're saying on the screen, side by side in English and Russian. the other side has the Russian mic, same thing. the transcript should scroll up as the conversation goes and should color code by mic speaker.”*

I used a DeepResearch ChatGPT call to get recommendations for what hardware to use.

---

## The Hardware

- **Raspberry Pi 4 + case** — ~$80  
  Works well here because it has two micro-HDMI ports for driving two screens.

- **USB gooseneck push-to-talk microphones** — ~$145 each  
  Pricey, but they have the exact push-to-talk functionality I wanted. They’re heavy enough to live permanently on a table and not slide around, and they make me feel like I’m in the UN.

- **SunFounder 7” LCD touchscreen displays** — ~$80 each  
  Big enough to read several back-and-forth statements at once.

---

## Cloud Dependencies

This project uses Google Cloud Speech-to-Text and the Google Translate API. Everything else runs locally on the Pi ([repo here]).

Speech-to-Text includes 60 free minutes per month, then costs about $1.44/hour. Translation costs roughly $20 per million characters. The rough math[^1] suggested we’d stay well within light usage, so I don’t expect this project to ever cost more than $10/month in cloud bills.

---

## Design Decisions & Tradeoffs

- **Cloud services**  
  This uses a cloud translation tool vs. an open source translation model. If I thought we’d use it enough that the cloud bills got hair-raising, I’d look into switching, but this solves our problems for now at an acceptable cost. It does mean this always needs a wifi connection to run..

- **Specified language microphones**  
  In this setup, one mic is always the English mic and one is always the Russian mic. This eliminates the need for any language detection, shaving off an API call and a little processing, but does mean we always have to sit at the same sides of the table. Because the mics have buttons, ChatGPT suggested a kind of button-based language toggling system (e.g. push the button twice to switch languages). Maybe in a v2..

- **Always-on screen**  
  I wanted this to be a convenient alternative to digging out a phone, so we leave the Pi on. The translator app boots at startup, so the Pi keyboard and mouse are packed away elsewhere. This has turned the translator into an old-fashioned college dorm whiteboard, in that we can leave messages for each other. I added a spoken phrase to clear the screen if needed (“system clear” in English, “система очистить” in Russian).

---

So, ChatGPT and I turned my dining table into a translator. I’d like to see how we use it for a while to know more about what’s missing, but a fun next version of this would be a portable translator box. I’m envisioning a container that holds the two screens on opposite faces with the wires and Pi hidden within.

---

[^1]: **Cost assumptions and math**

    **Speech-to-Text**
    
    - Average utterance length: 5 seconds  
    - One utterance every ~15 seconds  
    - ~240 utterances per hour (both speakers combined)

    Calculation:  
    240 × 5 seconds ≈ 1,200 seconds ≈ 20 minutes of audio per hour  
    20 minutes × ($1.44 / 60) ≈ **$0.48 per hour**

    **Translation**

    - ~10 words per utterance  
    - 240 utterances × 10 words = 2,400 words per hour  
    - ≈ 15,000 characters per hour

    Calculation:  
    15,000 / 1,000,000 × $20 ≈ **$0.30 per hour**

    **Total estimated cost**

    - Speech-to-Text: ~$0.48/hour  
    - Translation: ~$0.30/hour  
    - **Total: ~$0.80–$1.00 per hour**

    **Monthly examples**

    - Light use (10 hours/month): ~$8  
    - Regular use (50 hours/month): ~$40  
    - Daily use (2 hours/day): ~$60/month  
    - All-day kiosk use (8 hours/day): ~$180–200/month

