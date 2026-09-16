# Short Form Editor hiring form

This is the breakdown of the application form from the screen recording. It's a one question at a time, multi step form. One card in the middle of the screen, a title above it, a row of progress dashes at the top, Continue and Back buttons at the bottom of the card. Seven steps, then a success screen with confetti.

Nothing on the page is a normal landing page. No hero, no job description, no long scroll. The form is the whole page.

## The screens

The progress bar has 7 dashes. Six question steps plus the review step. Done steps are filled purple, the current step is a slightly longer purple dash, the rest are grey.

1. **Start here.** One question: which language will you use in this application. Two choice cards side by side, English and Russian, each with a small flag icon on the left and a circle on the right that turns into a purple check when picked. Required.

2. **Your work.** This step has three sub screens.
   First: "Do you have one example of your work with motion graphics and captions?" Two choice rows, Yes and "No, I want to do a sample edit". Under that there's a heading "Ideal short form video reference" with an embedded YouTube video (thumbnail with a purple play button, plays inline in the card).
   Second: a warning gate. A short paragraph saying more than one link or a full portfolio is an automatic disqualification, they only want one example. The only way forward is a checkbox button that says "I understand". It has a red outline and a red glow until you tick it, then it turns purple and lets you continue.
   Third: "Paste the link to the one example closest to the reference video". A single URL input with an https:// placeholder. Required.

3. **About you.** Name (required), Phone number (required, shows "Enter at least 10 digits" in small text on the right of the label if too short), Email (required), Telegram username (optional, @username placeholder), Discord username (optional), and "How well do you understand spoken English?" which is a slider from 0 to 10. The slider track has small dots at each step, fills purple as you drag, and the white knob shows the current number.

4. **Your editing stack.** "Which editing software do you use?" Checkbox rows: After Effects, Premiere Pro, CapCut, DaVinci Resolve, Other. Ticking Other reveals a "Type it in" input with a purple plus button. Typing something and hitting plus adds it as a new checked row above the input, and the input clears for the next one. If you try to add something that's already in the list the input border flashes red. Required, at least one.

5. **Subtitles.** "Do you automate your subtitles?" Yes or No. Picking Yes reveals a required textarea: "Please describe every step you take to generate your subtitles and be as detailed as you can", with a "Step one..." placeholder.

6. **Rate and delivery.** "Your price per reel (up to 45 seconds)", a number input with a $ prefix and USD suffix, required. "How many hours until you deliver the final file?", a number input, required. "Do you have a referral code?", optional, with a helper line underneath saying if somebody sent you put their code or name here, leave empty otherwise.

7. **Review your answers.** Every step becomes a summary card inside the main card. Each summary card has a purple check icon and the step name on the left, an Edit link with a pencil icon on the right, a thin divider, then each question in small grey text with the answer in white below it. Clicking Edit jumps back to that step. Under the summary cards there's a Cloudflare Turnstile widget (the "Verifying..." then "Success!" box). The button here says Submit instead of Continue, it's a solid purple pill with a glow, and it shows "Sending..." while the request is in flight.

8. **Success.** Confetti bursts from both sides in purple and white. A small card in the middle with a purple check circle, a big "Got it." headline, and a one line note under it saying the applications get read.

## How it looks

Background is #121212 with a faint warm glow at the top center. The card is a dark translucent grey (#1a1a1a) with a 1px border, 24px corners and a deep shadow, about 560px wide and centered. The step title sits above the card, white and bold.

The font is Montserrat everywhere.

The accent is your yellow, #ffde59. It's on the progress dashes, the selected state of every choice, the check icons, the Continue and Submit buttons, the slider fill, the plus button and the play button. Red (#ff5a4e) shows up in exactly two places: the "I understand" gate before it's ticked, and the input border when you try to add a duplicate tool or skip a required field.

Inputs are dark (#1e1e1e) with a 1px border and 12px corners. Focus gives them a yellow border and a soft yellow glow. Choice rows go yellow tinted with a yellow border when picked, and the check mark pops in.

Continue is a yellow pill with dark text and a dark circle holding a yellow arrow. Back is a round dark grey button. Submit is the same yellow pill with a glow.

Animations: the page fades up once on load. Each step slides in from the side (forward goes left, back goes right) while the card smoothly resizes to fit. Check marks spring in. Hidden fields expand open instead of popping. The gate button pulses red until ticked, then flips to yellow with a little bounce. Review cards stagger in. The success check pops and confetti bursts from both sides. All of it switches off if the visitor has reduced motion turned on.

## What it needs to actually work

The visual part is a single HTML file. Three things need a backend or a third party:

1. **Somewhere to send the submission.** Any endpoint that accepts a JSON POST. Formspree, Basin, Getform, a Zapier or Make webhook, a Google Apps Script web app, or your own server. Paste the URL into the config block.
2. **Cloudflare Turnstile.** Free. Create a widget in your Cloudflare dashboard, copy the site key into the config block. If you leave the key empty the Turnstile box is hidden and the form still submits, you just lose the bot check.
3. **A YouTube video ID** for the reference video on the "Your work" step.

Everything else runs in the browser. Answers are saved to localStorage as you go so a refresh doesn't wipe them.

## Files

`short-form-editor-form.html` is the form. Upload it to your domain as is. `prompt.md` is the full build prompt if you ever want it regenerated or changed. `short-form-editor.html` is the first landing page attempt, you can delete it.
