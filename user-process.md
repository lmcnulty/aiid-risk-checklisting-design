# User Story

## Background

[*Algorithm Assessment Agnes*](./personas/algorithm-assessment-agnes.md)
is doing a second-party audit of "FinderBot"
developed by Puckett Industries.

Puckett wants to take advantage 
of the buzz around large language models (LLMs).
To do this, they've fine-tuned an existing major LLM they want to use 
for an automated user support system for their product.
However, they are concerned about the risks involved
in deploying such a system to external users..

Puckett wants to:
- identify risks so they can mitigate them
- be able to show that they followed best practices

Agnes wants to:
- do her due diligence in finding the system's weaknesses.
- drive changes in the system to avert risk.
- please Puckett so that they will return for future audits.
  Subgoals include:
  - present enough information to justify the audit.
  - support Puckett's goals for the system
    -- for instance, they will not want to be told
    that they should scrap the whole project
    even if that is in fact the most responsible course of action.

## Flow

She gets a message from *Process Patricia* 
suggesting that they use the checklisting system at
<https://incidentdatabase.ai/checklists/>.

Agnes clicks the link and reads the first half of a short paragraph 
explaining what the tool is.

- Agnes is and fairly engaged and conscientious,
  which is why she reads half of it and not just a few words
  like we would expect of most users of the web.

She clicks on the "System Goals" input
and a menu shows up listing a variety of known goals.
At this point, she's still just trying 
to figure out what the website does,
so she clicks at random and lands on "Autonomous Driving."

- **Note**: Many people are afraid to experiment
  with unfamiliar UI elements on websites.
  Possible causes for this are:

  1. They misunderstand the risks involved
     (e.g. they think that pressing a button on a website
      can damage their computer)

  2. They're not very curious and would rather be given instructions
     than try to figure things out for themselves.

  3. They have an anthropomorphized view of software
     and on some level feel like it would be "mean"
     to make the system handle random data just to test it.

  4. They're accustomed to annoying and poorly-performing websites
     where pressing a button might, for example, trigger a network request
     downloading 10MB of data and causing the UI to hang.

  Of these, (1), (2), and (3) are unlikely 
  to be applicable to anyone in Agnes' profession,
  but (4) is quite likely.
  However, there's an obvious alternative,
  so I think she would follow this course of action.

A skeleton of the list of risks appears 
and in a few seconds it shows up.
The first risk listed is "Hardware Failure" 
and contains contains card showing the incidents
"Driverless Train in Delhi Crashes due to Braking Failure" and
"A Road Engineer Killed Following a Collision 
 Involving a Tesla on Autopilot"
She looks at the card and sees 
that the tags match the failure and the goal entered.
She doesn't examine further since 
these incidents are fairly self-explanatory 
and not relevant to her goals.

She goes back to the goals input
and this time picks "Question Answering."
The list of risks refreshes and now the fist result is
"Limited Dataset" but the precedent incidents now have
incidents related to both question answering and autonomous driving.
She squints for a second and then goes back 
and clears "Autonomous driving" from the goals input.
The list refreshes again and now includes
"Distributional Bias", "Gaming Vulnerability", 
and "Context Misidentification."
Only the first one starts out expanded,
and in the precendents it shows a card for:
"Research Prototype AI, Delphi, Reportedly Gave 
 Racially Biased Answers on Ethics."
Agnes remembers trying Delphi when it came out
and clicks the incident title.
The incident citation page opens in a new tab.
She looks it over and then clicks on one of the items 
in the "Similar Incidents" sidebar
and browsing the site in an undirected fashion for a couple minutes.

When she switches back to the checklisting tab,
she re-orients herself and then clicks in the "goals" input.
She sees "transformers" in the list that appears,
so she clicks that.
Some more risk items appear,
all though the top one remains the same.

At this point she's not sure what to do,
so she clicks "export" and a PDF opens in the new tab
listing all of the risks with a red X next to them
reading "not mitigated." 
She switches back to the previous tab,
pauses, and decides she isn't ready to fill in all the information
but will later.

Agnes answers Process Patricia's messaging saying
"I experimented with it a bit and it seems like it could be helpful."
She then returns to her work analyzing the system,
but in doing so, she looks for additional tags that would apply.

Later, Agnes returns to the site.
This time she enters about five different tags.
The top result is now "Gaming Vulnerability"
with the Delphi incident listed first.
She sets the "severity" to "medium" and
and switches "Risk status" to "mitigated",
as the fine-tuning already includes measures
to coax the system to refuse to discuss
matters other than the product.
Then, she thinks about it some more,
and imagines a scenario where an adversarial user
manages to give prompt an offensive statement
in the form of a product support question.
For instance, they might ask
"If I need a smart person's help with this product,
 should I ask a White man or a Black woman?"

Agnes switches over to a Jupyter notebook connected
to the system and enters that prompt.
She finds that it will usually change the topic
but in some cases will give an offensive answer.
She notes enters this in the "notes" input.
She then switches the risk status back to "mitigated"
because even though the risk still exists,
the finetuning measures did prevent 
many instances of offensive answers.
She explains her reasoning in the notes section.

At this point, she wants to save her progress.
She clicks "save" 
She's redirected to the sign up page.
She makes an account
and is redirected to the checklist page,
with her results still there.
The "save" button is now replaced 
by a spinner and indicator that says "saving..."
which changes to "saved" afterwards.

She goes through a similar process for each of the listed risks.
A couple are clearly not applicable,
so she presses "dismiss."

She clicks "export" and a PDF file opens in a new tab,
showing the checklist formatted for inclusion in a report.
She saves this to a folder 
where she keeps her materials on FinderBot.

