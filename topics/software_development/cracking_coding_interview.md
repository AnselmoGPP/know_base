# Cracking coding interview (synthesis)


## Table of Contents

* [References](#references)
* [Introduction](#introduction)
  * [Interview process](#interview-process)
  * [Behind the scenes](#behind-the-scenes)
  * [Special situations](#special-situations)
  * [Before the interview](#before-the-interview)
  * [Behavioural questions](#behavioural-questions)
  * [Big O](#big-o)
  * [Technical questions](#technical-questions)
  * [The offer and beyond](#the-offer-and-beyond)
* [Interview questions](#interview-questions)
  * [Arrays and Strings](#arrays-and-strings)
  * [Linked lists](#linked-lists)
  * [Stacks and Queues](#stacks-and-queues)
  * [Trees and Graphs](#trees-and-queues)
  * [Bit manipulation](#bit-manipulation)
  * [Math and Logic puzzles](#math-and-logic-puzzles)
  * [Object oriented design](#object-oriented-design)
  * [Recursion and Dynamic programming](#recursion-and-dynamic-programming)
  * [System design and Scalability](#system-design-and-scalability)
  * [Sorting and Searching](#sorting-and-searching)
  * [Testing](#testing)
  * [C and C++](#c-and-c++)
  * [Java](#java)
  * [Databases](#databases)
  * [Threads and Locks](#threads-and-locks)
  * [Moderate](#moderate)
  * [Hard](#hard)
* [Notes](#notes)
* [Technical patterns](#technical-patterns)
  

## References

- Gayle Laakmann McDowell (2015) _**Cracking the coding interview**_, 6th ed. CareerCup.


## Introduction

## Interview process

Algorithm and coding problems are problem-solving questions used for evaluating your ability to solve algorithmic problems you haven't seen before. Talk out loud throughout the problem and explain your thought process.

The interviewer **assess your performance** usually based on:

* Analytical skills
* Coding skills
* Technical knowledge / Computer Science fundamentals
* Experience
* Culture fit / Communication skills

**Reasons** for this process:

* False negatives are acceptable: Some good candidates may be rejected. Companies are more concerned on avoiding false positives.
* Problem-solving skills are valuable: They look for smart people.
* Basic data structure and algorithm knowledge is useful: Computer science knowledge might be useful, or at least it's a good "proxy". Also, it's hard to ask problem-solving questions that don't involve data structures and algorithms.
* Whiteboards let you focus on what matters: It allows you to focus on the big picture, and candidates  tend to speak more and explain their thought process.

**Selection of questions:** There are no lists of questions to ask. Each interviewer select its own questions. However, similar companies ask similar questions.

**Assessment:** It's a relative comparison. Interviewers assess you relative to other candidates on that same question by the same interviewer. He develops a feel for your performance by comparing you to all the candidates she's ever asked this question. Receiving a difficult question isn't bad, it's hard for everybody, which doesn't make it less likely that you'll do well.

**Candidate questions:**

* "I didn't hear back immediately after my interview. Am I rejected?": No. The company's decision might be delayed for different reasons (like one interviewer hasn't provided feedback yet). Very few companies don't respond to candidates they reject. If you haven't heard back from a company within 3-5 business days after the interview, check-in with your recruiter.
* "Can I re-apply to a company after getting rejected?": Almost always, after waiting a bit (6 months to 1 year). The first bad interview usually won't affect you too much when re-interviewed.


## Behind the scenes

Once you are **selected** for an interview, you usually go through a **screening interview**, which often involves coding and algorithm questions. You typically do 1 or 2 screening interviews before being brought on-site. In an **on-site interview** round you usually have 3-6 in-person interviews. One of them is usually not technical, and the interviewer may not even submit feedback (you can discuss your interests and ask about the company culture). The other interviews will be mostly technical and will involve a combination of coding, algorithm, design/architecture, and behavioural/experience questions. After your interview, your interviewers will provide feedback. Depending on the company, the **final decision** is made by your interviewers, a hiring manager, or a hiring committee. Most companies get back after about a week with next steps (offer, rejection, further interviews, or update). If you waited more than a week, you should follow up with your recruiter. Not receiving an answer indicates nothing about your status. Delays can and do happen.

**Microsoft:** It wants smart people passionate about technology. You'll show up at Microsoft in the morning and fill some paperwork. You'll have a short interview with a recruiter just to ease you. You'll do 4-5 interviews, often with 2 different teams. You'll meet the interviewers in their office. After completing the interviews with a team, you might speak with a hiring manager, which likely means that you passed the interviews with a team and it's now down to his decision. You might get a decision that day or in a week.

**Amazon:** It cares a lot about scalability and object-oriented design. It begins with a phone screen where an specific team interviews you. You will have to write simple code via a shared document editor, and answer questions about the technologies you know. Not often, you may have 2 or more interviews, which might indicate that one interviewer wasn't convinced or that you were considered for another team/profile. Next, you go to the office for 4-5 interviews with 1-2 teams where you will code on a whiteboard and show other skills. The recruiter usually follow up with you within a week.

**Google:** It cares about designing scalable systems, and analytical (algorithm) skills (regardless of experience). It begins with a phone screen, so expect tough technical questions which may involve coding. In the on-site interview you'll interview with 4-6 people. Feedback (based on analytical skills, coding, experience, and communication) is submitted to a hiring committee and managers to make a final recommendation. Making an offer can take several weeks because your packet goes through many stages and committees.

**Apple:** It looks for excellent technical skills, and passion for the position and the company. You should be familiar with the system. You usually start with a recruiter phone screen to know your skills, followed up by a series of technical phone screens with team members. Then, on-campus you will have 6-8 interviews with team members (including your future manager) and collaborators. You'll code on a whiteboard, so communicate your thoughts clearly. The final interview is with the director and the VP of the organization you're applying to. Your recruiter will usually follow up a few days later.

**Facebook:** It wants passionate people with entrepreneurial spirit that love building stuff fast and can hack elegant and scalable solution. It interviews developers for the company, not for specific teams. Once hired, you go through a 6-week "bootcamp". It begins with 1-2 technical phone screens involving coding. Then, you might get homework assignment involving coding and algorithms (care about coding style and peer review). In the on-site interviews, each interviewers has a role (behavioural, coding and algorithms, design/architecture). At the end, your interviewing team and a hiring manager discuss and submit a recommendation to the hiring committee.

**Palantir:** It looks for brilliant engineers. It interviews for a specific team. Usually you get 2 technical phone interviews of 30-45 minutes covering prior experience and algorithms. You might get a HackerRank coding assessment. Then, you will interview on-campus with up to 5 people covering prior experience, domain knowledge, data structures and algorithms, and system design. After this, interviewers discuss with the hiring manager.


## Special situations

**Experience candidates** usually receive the same algorithm-style questions as inexperienced candidates. However, they would be expected to give better responses for question about system design, architecture, and prior experience (resume).

**Testes and SDETs** (software design engineers in test) write code to test features instead of build them, so they're expected to be great coders and great testers. Strong communication skills are also very important. Practice core testing problems, coding questions, and also testing the coding questions (any problem can be an SDET problem).

**Product (and program) management** (PM) roles vary wildly. Some have customer-facing roles (bordering marketing) while others spend much of their day coding. Interviewers look for PMs with skills in:

* Handling ambiguity: Don't get overwhelmed or stall. Tackle the problem head on (seek for information, prioritize important parts, and solve problems in a structured way).
* Customer focus (attitude): Customer-focused attitude. Try to understand how customers want to use the product. Ask who the customer is and how they use the product.
* Customer focus (technical skills): Strong understanding of the product.
* Multi-level communication: Ability to communicate with people at all levels in the company.
* Passion for technology: Happy employees are productive employees. Companies wants you to enjoy the job and be excited about your work.
* Teamwork / Leadership: Ability to work well with other people. Companies want you to handle conflicts well, take initiative, understand people, and that people like working with you.

**Dev lead and Managers** require strong coding skills. Additionally, get prepared in:

* Teamwork / Leadership: Ability to both lead and work with people.
* Prioritization: Ability to prioritize a project appropriately, cutting the less important aspects. This requires asking the right questions to understand what is critical and what can reasonably expected to be accomplished.
* Communication: Ability to communicate at many levels, with people above and below you, and potentially with customers and other much less technical people.
* Getting things done: Striking the right balance between preparing for a project and actually implementing it. Understand how to structure a project and motivate people to accomplish the team's goals.

**Startups:** Their application and interview processes is highly variable. General points are:

* Application process: Many post job listings, but personal referral is preferred for the hottest startups. Often by reaching out and expressing interest, someone can pick up your resume.
* Visas and Work authorization: Many smaller startups in U.S. cannot sponsor work visas. You can focus on bigger startups or reach a professional recruiter who knows startups that work with visa issues.
* Resume selection factors: They smart engineers who can code, that have initiative (good for working in an entrepreneurial environment), and that already know the language of the company.
* Interview process: They often look closely at your personality fit, skill set, and prior experience. Coding and algorithms is also common.

**Acquisitions and Acquihires:** Before a company acquires a startup, the acquirer often interviews most or all of the startup's employees. Their employees have to go through this process to get hired. They held to the same standards as typical candidates, although there's a bit more leeway.

- Acquihires (talent acquisition) is about the employees or technology. Product acquisition is about the user base and community, which might omit the interview process. 
- These interviews have 3 purposes: make/break acquisition, determine which employees receive offers, and can affect the acquisition price.
- All engineers are usually interviewed, and probably any other role too. The CEO is often slotted into a product or dev manager interview.
- Employees who underperform don't receive offer (if too many underperform, the acquisition may fail), or maybe get a temporary contract for "knowledge transfer".
- Usually, existing teams are kept together as a team, or possibly integrated into an existing team.
- Some startups put work on hold and do interview prep for 2-3 weeks, though not all of them can do this. Team members should study individually, or in groups of 2-3, or by doing mock interviews with each other, or using the three approaches (recommended). Some people may be less prepared and will need more time to prepare. Don't wait until the last minute, acquisition interviews often come up very suddenly, so anticipate to this.

**Advices for interviewers:**

- Don't actually ask the exact questions in here. Questions that are good for interview preparation are not always good for interviewing. Also, candidates also read this and might have already solved your question before. Ask similar questions. You test their problem-solving skills, not their memorization skills.
- Ask medium and hard problems. Too easy questions make performance get clustered together. Minor issues can substantially drop someone's performance. It's not a reliable indicator.
- Look for questions with multiple hurdles, insights, or optimizations. Some questions rest on a particular insight (Eureka moment); if the candidate doesn't get that one bit, he will do poorly; if he get it, he will suddenly outperform other candidates.
- Use hard question, not hard knowledge. You should expect fairly straightforward data structure and algorithm knowledge. Expecting obscure knowledge reduce the focus on the skills you're looking for.
- Avoid scary questions. They intimidate candidates because it seems like they involve specialized knowledge (math, probability, low-level knowledge, system design, scalability, proprietary systems...), even if they really don't. Intimidated candidates might underperform.
- Offer positive reinforment. Make candidates feel comfortable, be warm and friendly. Nervous candidates will underperform. Candidates who had a bad experience might reject an offer and even dissuade their friends from interviewing/accepting.
- Probe deeper on behavioral questions. Many candidates are poor at articulating their specific accomplishments, so probe deeper, ask for more details.
- Coach candidates. You can offer tips (like how to develop good algorithms) to candidates who are struggling. They can fail in one area, but maybe that's not the only ability you want to evaluate. Guide them in these situations:
  - Many candidates don't use an example (or use a bad one) to solve a question, making it more difficult to get a solution.
  - Some candidates take too long to find a bug because they use a huge example. They might have not realized that a conceptual analysis or a small example could work well.
  - If they dive into code before having an optimal solution, pull them back and focus them on the algorithm.
  - They can get nervous and stuck, without knowing where to go. Suggest them a direction (like using a brute force solution and look for optimizations).
  - If they haven't said anything while there's a fairly obvious brute force, remind him that he can start off with a brute force. The first solution doesn't have to be perfect.
- If they want silence, give them silence. Give them time to think if they need it.
- Know your mode. There're 4 modes of questions:
  - Sanity check: Easy problem-solving or design questions. They assess a minimum degree of competence in problem-solving. Useful early in the process, or when minimum competency is needed.
  - Quality check: More challenging questions. They're rigorous and make candidates think. Useful when algorithmic/problem-solving skills are very important.
  - Specialist questions: They test knowledge of specific topics (Java, machine learning...). Useful for true specialists.
  - Proxy knowledge: Knowledge that is not specialist level, but that you expect a candidate at that level to know.


## Before the interview

Acing an interview starts well before the interview itself, years before. Process:

- **Get the right experience**. Without great experience, there's no great resume, and without a great resume, there's no interview. Companies want smart people that can code. Think in advance about where you want your career to go.

  - For students:
    - Seek out the classes with big coding projects to get practical experience.
    - Do everything you can to land an internship early in school. It will pave the way for better internships before graduating.
    - Build a personal project, participate in hackathons, or contribute to an open source project. This develops your skills and show initiative.

  - For professionals:
    - Shift work responsibilities more towards coding. Ensure these projects are "meaty", use relevant technologies, and fit well in your resume.
    - Use your free time (nights and weekends) to build software. Get experience with new technologies, and list this in your resume.

- **Write a great resume**. Highlight that you're smart and can code.

  - Keep resume to one page if you have less than 10 years of experience. Otherwise, you can have 1.5-2 pages. Prioritize content. Shorter resumes are often more impressive. Recruiters only spend about 10 seconds looking at your resume, and some people just refuse to read long resumes. 
  - Employment history: Your resume should include only the relevant positions that make you a more impressive candidate, not a full history of every role you had. Write strong bullets (_accomplished X by implementing Y which led to Z_). Show what your did, how you did it, and the results. Try to make results measurable somehow.
  - Projects: The project section present you as more experienced and shows initiative. Include your 2-4 most significant projects. State what the project was and the languages/technologies employed. 
  - Software: Include only relevant software.
  - Programming languages: You can list most of the languages you've used, adding your experience level (expert, proficient, prior experience...). The number of years of experience is a poor metric for resumes.
  - International:
    - Avoid typos. Some companies throw out your resume because of a typo.
    - For US position, don't include age, marital status, or nationality. This is not appreciated since it creates a legal liability for companies.
  - Potential stigma: Some languages have stigmas associated with them such as:
    - Enterprise languages: Those used for enterprise development. Example: Visual Basic or the .NET platform tend to be used to build not very sophisticated applications, so people will assume you're less skilled.
    - Being too language focused: It's believed in many circles that the best software engineers don't define themselves around a particular language.
    - Certifications: They can be positive, neutral, or negative. Some companies biased against candidates with too many technologies tend to also be biased against certifications.
    - Knowing only 1 or 2 languages: They can assume that you haven't experienced many problems, and that you may have trouble learning new technologies or feel too tied with a specific technology.

- **Preparation steps:** 

  - 1+ years (before interview):
    - Build projects outside school/work
    - Learn multiple programming languages
    - Expand network
    - Build website/portfolio showcasing your experience
    - Students: Find internship and take classes with large projects
    - Professionals: Focus work on "meaty" projects
  - 3-12 months:
    - Continue to work on projects. Try to add on one more project.
    - Create a draft of resume and send it out for a resume review
    - Make target list of preferred companies
    - Read intro sections of this text
    - Learn and master Big O
    - Implement data structures and algorithms from scratch
    - Form mock interview group with friends to interview each other
  - 1-3 months:
    - Do mini-projects to solidify understanding of key concepts
    - Do several mock interviews
    - Continue to practice interview questions
    - Create list to track mistakes you've made solving problems
  - 4 weeks:
    - Create interview prep grid
    - Review/update resume
    - Begin applying to companies
    - Re-read intro of this text, especially Tech & Behavioural section
    - Do another mock interview
    - Continue to practice questions, writing code on paper
  - 1 week:
    - Phone interview: Locate headset and/or video camera
    - Do a final mock interview
    - Rehearse stories from the interview prep grid
    - Re-read Algorithm approaches
    - Re-read Big O section
    - Continue to practice interview questions
  - Day before:
    - Rehearse each story from the interview prep grid once
    - Continue to practice questions & review your list of mistakes
    - Review Powers of 2 table. Print for a phone screen.
  - Day of:
    - Wake up in plenty of time to eat a good breakfast and be on time
    - Be confident (not cocky)
    - Remember to talk out loud. Show how you think.
    - Don't forget: Stumbling and struggling is normal
  - After:
    - Write Thank you note to your recruiter
    - If you haven't heard from recruiter, check in after one week
    - If no offer, ask when you can re-apply. Don't give up hope.


## Behavioural questions

They're asked to know your personality, understand your resume deeper, and ease you into an interview. Some things you can prepare are:

- **Interview preparation grid:** Go through each project or component of your resume and ensure that you can talk about them in detail.
  - You can fill an **interview grid**, a table with common questions (Y axis) and projects/jobs/activities (x axis). Study this grid before your interview. Common questions can be:

| Common questions                      | Project 1 | Project 2 | Project 3 |
|:--------------------------------------|:---------:|:---------:|:---------:|
| Challenges                            |           |           |           |
| Mistakes/failures                     |           |           |           |
| Enjoyed                               |           |           |           |
| Leadership                            |           |           |           |
| Conflicts                             |           |           |           |
| Technical decisions                   |           |           |           |
| Choices of technologies (& tradeoffs) |           |           |           |
| What you'd do differently             |           |           |           |

  - In addition, ensure that you have 1-3 project where you played a central role and that you can talk about in detail (technical components).
  - What are your weaknesses?: Give a real weakness, but emphasize how you work to overcome it.
  - What questions should you ask the interviewer?: Go into the interview with some questions in mind:
    - Genuine questions: Those you really want to know, like what the day-to-day life is at the company.
    - Insightful questions: They demonstrate your knowledge or understanding of technology. This typically requires advance research about the company.
    - Passion questions: They demonstrate your passion for technology. They show you're interested in learning and will be a strong contributor.

- **Know your technical projects:** You should focus on 2-3 technical projects that you should deeply master. Select projects that had challenging components (beyond just learning a lot), where you played a central role (ideally on the challenging components), and that you can talk about at technical depth. You can think about follow-up questions (like how you would scale the application).

- **Responding behavioural questions:** They're used to get to know you and your prior experience better.

  - Be specific, not arrogant. Just give the facts and let the interviewer derive an interpretation (like, instead of saying that you did all the hard parts, you can describe the specific challenging bits you did).
  - Limit details. Just state the key points. The interviewer might not be well versed in the subject or project to understand it. When possible, try to translate, or at least explain the impact. You can always offer to drill in further.
  - Focus on yourself, not your team. Otherwise, the interviewer may have little idea of your impact and might conclude you did little.
  - Give structured answers. There're 2 techniques for this (can be used separately or together):
    - Nugget first: Start with a "nugget" that succinctly describes what your response will be about. This grabs the attention, makes clear what your story is about, and helps you to focus.
    - Situation, action, result (SAR): First, outline the situation, then explain the actions you took, and then describe the result. Situation and result should be succinct. This make easy identify how you made an impact and why it mattered. You can put your stories in this grid:

|         | Nugget | Situation | Action/s | Result | What it says |
|:--------|:-------|:----------|:---------|:-------|:-------------|
| Story 1 |        |           | 1. …     |        |              |
|         |        |           | 2. …     |        |              |
|         |        |           | 3. …     |        |              |
| Story 1 |        |           |          |        |              |

  - Explore the action. The action is the most important part of the story, so dive into it. If possible, break down the actions into multiple parts ("_I did 3 things. First, I…").
  - Think about what it says. Analyse your actions and how you reacted in your story to know what personality attributes your reaction demonstrates (initiative/leadership, empathy, compassion, humility, teamwork/helpfulness). Learn how to communicate the story to make your attributes clearer. If you cannot do it, maybe you need to come up with a new story entirely.

- **Tell me about yourself:** This is usually asked to get the first impression of you.

  - Structure: A chronological one usually works well.
    - Current role: Just an opening sentence…
    - College: Studies, projects, experiences…
    - Post college & onwards: Working experience, objectives…
    - Current role: Give details.
    - Outside of work: Projects, hackathons, forums…
    - Wrap up: Reasons to change, interests…
  - Hobbies: If it's generic activities (skiing, playing with your dog…), you can probably skip it. But sometimes they can be useful, which often happens when it's extremely unique (fire breathing), is technical (it boosts your skillset and shows passion for technology), or demonstrates a positive personality attribute (remodelling your house yourself).
  - Sprinkle in shows of successes. You can casually drop in some highlights of your background. Know what your pitch tells about aspects of your background.


## Big O

### Time complexity

**Big O time**, or **asymptotic runtime**, is the language and metric to describe the efficiency of algorithms. Most common runtimes are: O(1), O(n), O(log n), O(n log n), O(n), O(n<sup>2</sup>), and O(2<sup>n</sup>). Derive the runtime, don't guess it.

Given a O(1) (constant time) algorithm and a O(n) (linear time) algorithm, it doesn't matter how big the constant is and how slow the linear increase is, linear will surpass constant at some point.

Examples:

- Sending a file of size s by email takes O(s) time (the bigger the file, the longer it takes), but sending it by airplane takes O(1) time (it always takes the same amount of time).
- Painting a wall of width w and height h takes O(wh) time, but applying p layers of paint takes O(whp).

**Academics** describe runtimes using big O, big Θ (theta), and big Ω (omega). In academia, they mean:

- __Big O__: Upper bound on the time. An algorithm that prints all values from an array can be described as O(n), or any other time bigger than O(n), like O(n<sup>2</sup>), O(n<sup>3</sup>), or O(2<sup>n</sup>).
- __Big Ω__ (omega): Lower bound on the time. Printing all values from an array is Ω(n), or any other time lower than Ω(n), like Ω(log n), or Ω(1).
- __Big Θ__ (theta): Tight bound on runtime. It's both O and Ω. An algorithm is Θ(n) if it's O(n) and Θ(n).

In **industry**, the meaning of big O is closer to the academic meaning of Θ: the tightest runtime.

**Cases**: The runtime of an algorithm (example: Quick Sort) can be describe in 3 ways.

- **Best case**: If all elements are equal, Quick Sort will, on average, traverse the array once (O(n)). However, this depends on the implementation.
- **Worst case**: If the Quick Sort pivot is repeatedly the biggest element in the array, it will cause a O(n<sup>2</sup>) runtime.
- **Expected case**: What we can usually expect from Quick Sort is a O(n log n) runtime.

Worst case is not very useful, so it's rarely discussed. For most algorithms, the worst and expected case are the same. Sometimes they're different and we need to describe both runtimes. Best/worst/expected case and big O/Ω/Θ have no particular relationship:

- Best/worst/expected cases describe big O time for particular inputs/scenarios.
- Big O/Ω/Θ describe the upper/lower, tight bounds for the runtime.

### Space complexity

Similar to time complexity, but with the space required. Creating an array of size n require O(n) space. Creating a 2D array of size nxn require O(n<sup>2</sup>) space. 

In **recursive calls**, stack space counts. Each call is added to the call stack (new level is added), which takes up actual memory. The following function takes O(n) time and O(n) space:

```
int sum(int n)
{
  if(n <= 0) return 0;
  return n + sum(n-1);
}
```

However, having n calls doesn't mean it takes O(n) space. The following function takes O(n) time and O(1) space because the calls doesn't exist simultaneously on the call stack:

```
int pairSumSequence(int n)
{
  int sum = 0;
  for(int i = 0; i < n; i++)
    sum += pairSum(i, i+j);
  return sum;
}

int pairSum(int a, int b) { return a + b; }
```

### Drop the constants

It's possible for O(n) code to run faster than O(1) for specific inputs. Big O just describes the rate of increase. Thus, we drop the constants in runtime. An algorithm described as O(2n) is actually O(n). Not doing this doesn't make you more precise. Big O express how runtime scales, which doesn't mean that O(n) is always better than O(n<sup>2</sup>).

### Drop non-dominant terms

Examples:

- O(n<sup>2</sup> + n) → O(n<sup>2</sup>)
- O(n<sup>2</sup> + n<sup>2</sup>) → O(n<sup>2</sup>)
- O(n + log n) → O(n)
- O(5·2<sup>n</sup> + 1000 n<sup>100</sup>) → O(n<sup>2</sup>)

We might still have sum in a runtime. For example, O(B<sup>2</sup> + A) cannot be reduced (without special knowledge of A and B).

Rates of increase of common big O times:

<br>![design patterns table](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/rates_of_increase.png)

### Multi-part algorithms: Add vs. Multiply

If your algorithm has 2 steps, you have to add or multiply the runtimes.

- Add (O(A+B)): Do A first and, when you are done, do B.
- Multiply (O(A·B)): Do B for each time you do A.

### Amortized time

A dynamically resizing array (`std::vector`) is an array whose capacity increases as you insert elements. When it hits capacity, it creates a new array with double the capacity and copy all elements over to the new array. Describing the runtime of insertion here is tricky. It usually takes O(1) time, but sometimes (when the array is full) it takes O(n).

**Amortized time** takes both situations into account. It describe situations where a worst case happens every once in a while, but once it happens, it won't happen again for so long that the cost is "amortized".

In a dynamic array we double capacity when the array size is a power of 2. After X elements, we double capacity at array sizes 1, 2, 4, 8, 16, … X. This doubling takes, respectively, 1, 2, 4, 8, 16, 32, 64, … X copies.

- 1 + 2 + 4 + 8 + 16 + … + X  =  X + X/2 + X/4 + X/8 + … 1  =  ~2X

Therefore, X insertions take O(2X) time. The amortized time for each insertion is O(1).

### Log n runtimes

When the number of elements in the problem space gets halved each time, that will likely be O(log n) runtime.

- log<sub>2</sub>X = Exponent of a power of 2 that values X.
  - 2<sup>B</sup> = A
  - log<sub>2</sub>A = B

Example: In a balanced binary search we look for x in an n-element sorted array. We first compare x to the array midpoint. If `x == middle`, we return. If `x < middle`, we search on the left side of the array. If `x > middle`, we search on the right side. We start off with an n-element array to search. After one step, we're down to n/2, then n/4, and so on. We cut the problem space in half each time. We stop when we find the value or we're down to just one element. This search takes O(log n) time.

What is the base of the log? It doesn't matter for the purposes of big O because logs of different bases are only different by a constant factor.

### Recursive runtimes

```
int f(int n)
{
  if(n <= 1) return 1;
  return f(n-1) + f(n-1);
}
```

This function forms a binary tree of calls of depth n. Thus, each level has twice as many calls as the one above it. Each level has 2<sup>level</sup> nodes.

- Total number of nodes  =  2<sup>0</sup> + 2<sup>1</sup> + 2<sup>2</sup> + … + 2<sup>n</sup>  =  2<sup>n+1</sup> - 1

Recursive functions that make multiple calls often (but not always) have runtime O(branches<sup>depth</sup>), where branches is the number of times each recursive call branches. Our example is O(2<sup>n</sup).

The base of the exponent matters because base differences are not different by a constant factor. Example: 2<sup>n</sup> and 8<sup>n</sup> are different by a factor of 2<sup>2n</sup>, which is not a constant factor.

- 8<sup>n</sup>  =  2<sup>3n</sup>  =  2<sup>n</sup> · 2<sup>2n</sup>

The space complexity of our algorithm is O(n) space because, though we have O(2<sup>n</sup>) nodes in total in the tree, only O(n) exist at any given time. 

### Examples

```
void printPairs(int[] array)
{
  for(int i = 0; i < array.length(); i++
    for(int j = i+1; j < array.length; j++)
      print(array[i], array[j]);
}
```

- (n-1) + (n-2) + (n-3) + … + 2 + 1  =  1 + 2 + 3 + … + n-1  =  n(n-1) / 2
- O(n n(n-1)/2)  =  O(n<sup>2</sup>)

```
void printPairs(int[] arrayA, int[] arrayB)
{
  for(int i = 0; i < arrayA.length; i++)
    for(int j = 0; j < arrayB.length; j++)
      print(arrayA[i], arrayB[j]);
}
```

- O(ab)

```
// Algorithm that takes an array of strings, sorts each string, and then sorts the full array
```

- Sort one string = O(s log s)   (s = length of longer string)
- Sort all strings = O(a s log s)   (a = number of strings in the array)
- Compare strings = O(s)
- Sort array of strings = O(a s log a)
- O(a s log s + a s log a)  =  O(a s (log s + log a))

```
Boolean isPrime(int n)
{
  for(int i = 2; i * i <= n; i++)   // (i*i <= n) == (i <= sqrt(n))
    if(n % i == 0) return false;
  return true;
}
```

- This methods only needs to go up to √n because if n is divisible by a number greater than √n then it's divisible by something smaller than it.
- O(√n)

```
int factorial(int n)
{
  if(n < 0) return -1;
  else if(n == 0) return 1;
  else return n * factorial(n-1)
}
```

- O(n)   (it's a straight recursion)

```
void permutation(string str) { permutation(str, ""); }

void permutation(string str, string prefix)
{
  if(str.length() == 0) print(prefix);
  else
    for(int i = 0; i < str.length(); i++)
	{
	  string rem = str.substring(0, i) + str.substring(i + 1);
	  permutation(rem, prefix + str.charAt(i));
	}
}
```

- How many times does `permutation` get called in its base case? We pick character for each "slot". If we have 7 characters, in the first slot we have 7 choices. Once we pick the letter there, we have 6 choices for the next slot. Then 5 for the next, and so on. Thus, there're n! permutations. Function `permutation` is called **n!** times in its base case (when `prefix` is the full permutation).
- How many times does `permutation` get called before its base case? Consider how many times the for-loop block is executed. Picture a large call tree representing all the calls. There're n! leaves, as shown above. Each leaf is attached to a path of length n. Thus, there won't be more than **n·n!** nodes (function calls) in this tree.
- How long does each function call take? Executing `print(prefix)` takes O(n) time since each character is printed. The for-loop block take O(n) time combined, due to string concatenation (the sum of the lengths of `rem`, `prefix`, and `str.charAt(i)` will always be n. Thus, each node in our call tree corresponds to O(n) work.
- Total runtime: Since we call `permutation` O(n·n!) times (as an upper bound), and each one takes O(n) time, the total runtime won't exceed **O(n<sup>2</sup>·n!)**.

```
int fibonacci(int n)
{
  if(n <= 0) return 0;
  else if(n == 1) return 1;
  return fibonacci(n - 1) + fib(n - 2);
}
```

- O(branches<sup>depth</sup>)  =  O(2<sup>n</sup>)
- Actually, it's O(1.6<sup>n</sup>) (complicated math is needed) because at the bottom of the call stack sometimes there's only one call.
- An algorithm with multiple recursive calls generally has exponential time.

```
void allFib(int n)
{
  for(int i = 0; i < n; i++)
    print(i, fib(i));
}

int fib(int n)
{
  if(n <= 0) return 0;
  else if(n == 1) return 1;
  return fib(n - 1) + fib(n - 2);
}
```

- `fib(n)` takes O(2<sup>n</sup>) time, but `allFib(n)` is not just O(n·2<sup>n</sup>) because it calls `fib` with different values.
- `allFib` takes 2<sup>1</sup> + 2<sup>2</sup> + 2<sup>3</sup> + … + 2<sup>n</sup>  =  2<sup>n+1</sup>  =  O(2<sup>n</sup>)

```
void allFib(int n)
{
  int[] memo = new int[n + 1];
  for(int i = 0; i < n; i++)
    print(fib(i, memo));
}

int fib(int n, int[] memo)
{
  if(n <= 0) return 0;
  else if(n == 1) return 1;
  else if(memo[n] > 0) return memo[n];

  memo[n] = fib(n-1, memo) + fib(n-2, memo);
  return memo[n];  
}
```

- Process:

  - `fib(1)` → return `1`
  - `fib(2)`
    - `fib(1)` → return `1`
    - `fib(0)` → return `0`
    - store `1` at `memo[2]`
  - `fib(3)`
    - `fib(2)` → lookup `memo[2]` → return `1`
    - `fib(1)` → return `1`
    - store `2` at `memo[3]`
  - `fib(4)`
    - `fib(3)` → lookup `memo[3]` → return `2`
    - `fib(2)` → lookup `memo[2]` → return `1`
    - store `3` at `memo[4]`
  - `fib(5)`
    - `fib(4)` → lookup `memo[4]` → return `3`
    - `fib(3)` → lookup `memo[3]` → return `2`
    - store 5 at `memo[5]`
  - …

- At each call to `fib(i)`, already computed and stored `fib(i-1)` and `fib(i-2)`. We just look up those values, sum them, store the result, and return. This takes a constant amount of time. We do a constant amount of work n times, so this is O(n) time.
- Memoization: Technique to optimize exponential time recursive algorithms.

```
int powersOf2(int n)
{
  if(n < 1) return 0;
  else if(n == 1) { print(1); return 1; }
  else
  {
    int prev = powersOf2(n/2);
	int curr = prev * 2;
	print(curr);
	return curr;
  }
}
```

- This prints all the powers of 2 between 1 and n. There're log n powers of 2 between 1 and n. Thus, runtime is O(log n)

- Process:

  - `powersOf2(25)
    - `powersOf2(12)
	  - `powersOf2(6)
	    - `powersOf2(3)
		  - `powersOf2(1)
		    - print & return `1`
		  - print & return `2`
		- print & return `4`
	  - print & return `8`
    - print & return `16`
  - print & return `32`

- Runtime is the number of times we can divide n by 2 until getting the base case (1). This is O(log n).

- The number of calls to `powersOf2` increase by 1 if n doubles in size. Thus, the number of calls to `powersOf2` is the number of times you can double 1 until you get n, which is x in the equation 2<sup>x</sup> = n. And x = log n. Thus, runtime is O(log n).


## Technical questions

### How to prepare

Just reading problems and its solutions whon't help much. You've to practice solving problems. For each problem:

- Try to solve it on your own, and think about space and time efficiency.
- Write the code on paper. This doesn't offer special tools (syntax highlighting, code completion, quick debugging…) and makes writing/editing code slow.
- Test your code on paper (general cases, base cases, error cases…).
- Type your paper code as-is into a computer. Make a list of all the errors you make so you can keep them in mind.

Try to do as many mock interviews as possible with. You and a friend can take turns giving each other interviews. He can walk you through a coding/algorithm problem, and you can learn a lot from experiencing what it's like to be an interviewer.

### What you need to know

The data structure and algorithm interview questions are not knowledge test, but they assume a baseline of knowledge. Absolute essentials are:

- Core data structures:
  - Linked lists
  - Trees, Tries, Graphs
  - Stacks & Queues
  - Heaps
  - Vector/ArrayLists
  - Hash tables
- Algorithms
  - Breadth-first search
  - Depth-first search
  - Binary search
  - Merge Sort
  - Quick Sort
- Concepts
  - Bit manipulation
  - Memory (Stack vs. Heap)
  - Recursion
  - Dynamic programming
  - Big O time & space
- Powers of 2 table: Useful for questions about scalability or memory limitation. 
  
| Power of 2 | Exact value (X)   | Approx. value | X bytes in memory |
|:----------:|:-----------------:|:-------------:|:-----------------:|
| 7          | 128               |               | 16 bytes          |
| 8          | 256               |               | 32 bytes          |
| 10         | 1024              | 1 thousand    | 1 KB              |
| 16         | 65,536            | 65 thousand   | 64 KB             |
| 20         | 1,048,576         | 1 million     | 1 MB              |
| 30         | 1,073,741,824     | 1000 million  | 1 GB              |
| 32         | 4,294,967,296     |               | 4 GB              |
| 40         | 1,099,511,627,776 | 1 billion     | 1 TB              |

Data structures, algorithms and conceps: You're expected to know the basics, not specific algorithms for binary tree balancing or other complex algorithms. For each topic, you must understand how to use and implement them, and the space and time complexity, if applicable. Practice implementing them on paper and on computer.

Example of table use: To quickly compute that a bit vector mapping every 32-bit integer to a boolean value could fit in memory of a typical machine. There're 2<sup>32</sup> such integers. Each integer takes 1 bit in this bit vector, so we need 2<sup>32</sup> bits (= 2<sup>32</sup> / 2<sup>3</sup> = 2<sup>29</sup> bytes) to store this mapping. That's about half GB, which is easily available on a typical machine.
 
### Problem walkthrough

Keep talking while working on a problem. The interviewer wants to know your thought process. Also, interviews are supposed to be difficult. It's ok if you don't get an answer immediately.

How to solve a problem: Listen > Example > Brute force > Optimize > Workthrough > Implement > Test.

- **Listen**: Pay very close attention to any information in the problem description. You probably need it all for an optimal algorithm. Don't forget any key detail. Ask question about anything you're unsure about.

- **Draw an example**: An example can dramatically improve the ability to solve a question, unlike solving it in your head. Choose a good example. Most examples are too small or are special cases, so debug and fix your example if necessary. It has to be:
  - __Specific__: Use real numbers or strings, if applicable.
  - __Sufficiently large__: Most examples are too small, by ~50%. Too small examples prevent you from discovering patterns.
  - __Not special case__: It's easy to draw one inadvertently. 

- **State a Brute force**: Get a brute-force solution, and its runtime, as soon as possible. Don't code it or worry about efficiency yet. It's a starting point for optimizations and help wrap your head around the problem.

- **Optimize**: Walk through your brute force trying this:
  - Look for unused info. You usually need it all.
  - Solve it manually on an example, then reverse engineer your thought process. How did you solve it? Using a different example can help.
  - Solve it "incorrectly" and then think why it fails. Can you fix those issues?
  - Make time vs. space tradeoff. Storing extra state can help optimize the runtime. Hash tables are especially useful.
  - Precompute information. Reorganizing data or computing some values upfront may help save time.
  - Use hash tables. They're widely used in interview questions.
  - Think about the best conceivable runtime.
  - Look for BUD optimization (Bottlenecks, Unnecessary work, Duplicated work).

- **Walkthrough**: Before coding, walk through your optimal solution in detail making sure that you understand each detail. This makes implementation easier and prevent major errors. You can write pseudocode, but the for loops are probably better as code than as pseudocode.

- **Implement**: Code your optimal solution. Write beautiful code. Recommendations:
  - __Modularized code__: Shows good coding style and makes things easier for you. Example: if your algorithm uses a matrix initialized in a certain way, don't waste time writing the initialization code, just pretend you have a function that does it, and fill in the details later if needed.
  - __Refactor code__: If you see something you can refactor later on, explain it to the interviewer and decide whether or not it's worth the time to do so.
  - __Error checks__: You can write a `todo` and then explain out loud what you'd like to test.
  - __Pretend you've appropriate classes/structs__. Example: if a function needs to return a list of start and end points, just pretend that class `StartEndPair` exists. You'll deal with details later if you've time.
  - __Good variable names__: They make code more readable. Long variable names can be slow to write, but most interviewers allow you to abbreviate it after the first usage (`startChild` → `sc`).

- **Test**: You should test your code before submitting it. Rather than using your earlier example to test you code, which will take a long time, try this:
  - __Conceptual test__: Read and analyze what each line of code does. It's like explaining the lines to a code reviewer.
  - __Check weird looking code__: You might have writen it for a reason, but check that it's right. Example: `x = length - 2`.
  - __Hot spots__: Check the things that are likely to cause problems (base cases in recursive code, integer division, null nodes in binary trees, start and end of iteration through linked lists…).
  - __Small test cases__: First test using and actual and specific test case. Don't use a big example.
  - __Special cases__: Test code agains special cases (null or single element values, extreme cases…).
  - If you find bugs, fix them. Don't make the first correction you think of; instead, carfully analyze the cause of the bug and ensure your fix is the best one.

### Optimize & solve technique: BUD (Bottlenecks, Unnecessary work, Duplicated work)

You can walk through you brute force looking for BUD (Bottlenecks, Unnecessary work, Duplicated work). If you find one of these things, get rid of it. Repeat this approach until your algorithm is optimal.

- **Bottlenecks**: Part of the algorithm that slows down the overall runtime.
  - Common sources:
    - There's one-time work that slows down the algorithm. Example: in a two-step algorithm that first takes O(n log n) and then O(n), the priority is optimizing the first part (bottleneck). The second part doesn't matter too much.
	- There's a work that is done repeatedly (like searching). Perhaps this can be reduced from O(n) to O(log n) or O(1).
  - Example:
    - Given an array of distint integer values, count the number of pairs that have difference k.
	- Brute force: Traverse the array and, for each element, search the remaining elements. The second search is the bottleneck. Runtime: O(n<sup>2</sup>).
	- First optimization: We can sort the array, traverse it and, for each element, do a binary search (two-step algorithm). Sorting is the new bottleneck. Runtime: O(n log n + n log n) = O(n log n).
	- Second optimization: Modify first step. Copy the array content into a hash table (unsorted array). Lookup now is O(1). Runtime: O(n)

- **Unnecessary work**: Example:
  - Print all positive integer solutions to equation _a<sup>3</sup> + b<sup>3</sup> = c<sup>3</sup> + d<sup>3</sup>_, where a, b, c, d are integers in range [1, 1000].
  - Brute force: Iterate through all combinations of a, b, c, d (4 nested for-loops) and check if the combination works. Runtime: O(n<sup>4</sup>).
  - There's only one correct d value, so there's no need to continue searching d values once we found the correct one (`break` the loop). Runtime: O(n<sup>4</sup>).
  - There's only one correct d value, so we can just compute it (d = <sup>3</sup>√(a<sup>3</sup> + b<sup>3</sup> + c<sup>3</sup>)) instead of searching for it. Runtime: O(n<sup>3</sup>).

- **Duplicated work**: Example:
  - Consider the same problem and brute force algorithm as above. It iterates through all (a, b) pairs and then search all (c, d) pairs.
  - We can compute all values of all (c, d) pairs (c<sup>3</sup> + d<sup>3</sup>) and store them into a hash table that maps from the sum to the list of pairs that have that sum (`unsorted_map<int, vector<pair<int, int>>>`). Now, given a sum a<sup>3</sup> + b<sup>3</sup>, we can find quickly the corresponding (c, d) pairs.
  - Actually, having the map of all (c, d) pairs, we don't need to generate the (a, b) pairs. We can just traverse the map and get all the combinations of pairs for each pair. Runtime: O(n<sup>2</sup>).

### Optimize & solve technique: DIY (Do It Yourself)

Given an actual example, our intuition can give us a very nice algorithm (example: somebody that knows nothing about binary search still can use a dictionary book and lookup a word very quickly). Thus, when you get a question, try just working it through intuitively (manually) on a good example. Often a bigger example will be easier. Then, think about how you solved it and reverse engineer your approach. Be aware of any "optimizations" you intuitively or automatically made.

Example: Given a smaller string s and a bigger string b, find all permutations of the shorter string within the longer one. Print the location of each permutation.

- Permutation: Rearrangements of the string, so the characters in s can appear in any order in b. They must be contiguous.
- Most people would generate all permutations of s and then lok for each in b. This takes O(s! b) time (extraordinarily slow).
- However, when trying to solve this manually, most people walk through b looking at sliding windows of `s.length` characters, checking it it's a permutation of s. This takes O(b s).

### Optimize & solve technique: Simplify and Generalize

First, simplify/tweak some constraint (such as the data type); then, solve this new simplified problem; finally, try to adapt it for the more complex problem.

Example: Figure out if a certain message (string) can be formed from the words in a given text (string).

- Simplification: Modify it so that we are taking characters out of the text instead of words. We can solve this by creating an array and counting the characters (we count the number of times a character appears both in the message and the text).
- Generalization: We do a similar thing, but using a hash table that maps a word to its frequency.

### Optimize & solve technique: Base case and Build

First, solve the problem for a base case (like n=1); then, try to build up form there. We try to build more complex cases using prior solutions. Base case and Build algorithms often lead to natural recursive algorithms.

Example: Print all permutations of a string. For simplicity, assume all characters are unique.

- Case "a" = { "a" }
- Case "ab" = { "ab", "ba" }
- Case "abc" → Insert "c" into all locations of all strings in case "ab" (i.e., "ab" and "ba").
- Understanding the pattern we can develop a general recursive algorithm that iterates through all permutations of length n and, for each permutation, inserts the next character into all positions, creating all permutations of length n+1.

### Optimize & solve technique: Data structure brainstorm

Run through a list of data structures and try to apply each one. Sometimes, using a certain data structure makes the problem trivial to solve.

Example: Numbers are randomly generated and stored into an expanding array. How would you keep track of the median?

- Linked list? No, it's not good for accessing and sorting numbers.
- Array? Maybe. We already have an array. Keeping elements sorted is probably expensive. Let's hold off on this for now.
- Binary tree? It's possible. It's good ordering. If it's perfectly balanced, the top might be the median. But if there's an even number of elements, the median is the average of the middle two elements, and two elements cannot both be at the top.
- Heap? It's good at basic ordering and keeping track of max and mins. Having two heaps you can keep track of the bigger half (in a min-heap, so its smaller element is at the root) and the smaller half (in a max-heap, so its biggest element is at the root) of the elements. The potential median elements are at the roots. If heap have no longer the same size, you can quickly rebalance them by popping an element off one heap and pushing it onto the other.

### Best Conceivable Runtime (BCR)

**BCR**: Best runtime you could conceive of a solution ot a problem having. You can easily prove that there's no way you could beat the BCR. The BCR is not necessarily achievable, it only says that you can't do better than it. The BCR is for a problem, it's a function of the inputs and outputs, and has no connection to a specific algorithm. Don't confuse BCR with **Best Case Runtime**, which is for a specific algorithm, and is a mostly useless value.

- Example: Compute the number of element that two arrays, of length A and B, have in common. You know that you can't do that better than O(A+B) time because you have to touch each element in each array, so BCR = O(A+B).

- Example: Print all pairs of values within an array. You know you can't do this better than O(n<sup>2</sup>) time because there're n<sup>2</sup> pairs to print, so BCR = O(n<sup>2</sup>).

- Example: Find all pairs with sum k within an array, assuming all distinct elements. You might think BCR is O(n<sup>2</sup>) because you have to look at n<sup>2</sup> pairs, but this is false. Just because you want all pairs with a particular sum doesn't mean you've to look at all pairs.

- Example: Given 2 sorted arrays of same length, each having all distinct elements, find the number of elements in common. The BCR is O(n) because we know we have to look at each element at least once and there are 2n total elements.
  - Brute force algorithm: Traverse A and search (linearly) for each element in B, which takes O(n<sup>2</sup>) time.
  - We want to do better than O(n<sup>2</sup>) potentially, but not necessarily as O(n).
  - __BCR gives us a hint for what we need to reduce__. Given our O(n·n) runtime, maybe we can reduce the second O(n) to O(1) or O(log n). Since they're sorted arrays, we can do a binary search, getting a total O(n log n) time. In general, we cannot search an array better than O(log n) time.
  - __BCR indicates where we should look for improvements__. BCR tells that it cannot be faster than O(n). Therefore, any work in the O(n) time won't impact our runtime, so improving it isn't a priority. We should focus on reducing the O(log n) search.
  - We can throw everything in B into a hash table (O(n)). Then, we traverse A and look up each element in the hash table (O(n · 1)). Total runtime: O(n + n) = O(n).
  - __BCR tells us when we're done with runtime optimizations, and we should turn to work on the space complexity__. We cannot optimize big O time anymore, but we could potentially optimize space complexity.
  - Note that the arrays were sorted, but we would achieve the same runtime if they weren't. So why did the interviewer give us sorted arrays?
  - O(n) space is used. Maybe we can get O(1) space, which means that we have to drop the hash table. Probably, it can still take O(n) time. Let's use the fact that the arrays are sorted.
  - BUD → The bottleneck is the searching. It's not necessary to search all elements from A all over B. Each binary search should start where the last one left off. In fact, we can do a linear search instead, where the search in B picks up where the last one left off. This takes O(1) space and O(n) time. Big O time or space cannot be optimized.

### Handling incorrect answers

It's not true that candidates need to get every question right. It's not about whether the question is correct or incorrect. Everybody make mistakes, even those that get offers.

- It's about how optimal the final solution is, how long it took, how much help was needed, and how clean was the code.
- A candidate is evaluated in comparison to other candidates, so the difficulty of the questions doesn't matter.
- Many/most questions are too difficult to expect even a strong candidate to immediately get the optimal algorithm.

### When you've heard a question before

If you've heard a question before, admit this to your interviewers. Otherwise, he won't be able to evaluate you and he may find it highly dishonest. Admitting it will allow him to evaluate your problem-solving skills and you will get big honesty points. 

### The "perfect" language for interviews

Many companies aren't picky about programming languages, they just want to know how well you solve problems. Other companies want to see how well you can code in a particular language. If possible, you should probably pick whatever language you're most comfortable with. If you have several good languages, keep in mind:

- __Prevalence__: It's not required, but ideal that your interviewer knows the language you use.
- __Language readability__: Even if the interviewer doesn't know you language, they should be able to basically understand it. Example: C, C++, or Java are more understandable than Scala or Objective C.
- __Potential problems__: Some languages open you up to potential issues. Example: C++ can have memory management and pointer issues.
- __Verbosity__: Some languages are more verbose than others. Example: Java is more verbose than Python. However, verbosity can be reduced by abbreviating code, which most interviewers wouldn't mind as long as you explain the abbreviations.
- __Ease of use__: Some operations are easier in some languages than others. Example: Python functions can return multiple values, but Java functions would require a new class. However, this can be mitigates by abbreviating code or presuming methods that you don't have.

### Good coding

Employers want to see you writing good, clean code. Good code properties are:

- __Correct__: Operates correctly on all expected and unexpected inputs.
- __Efficient__: Operates as efficiently as possible in time and space, including both the asymptotic (big O) efficiency and the practical efficiency (constant factors that matter).
- __Simple__: Use the least possible lines. Code should be as quick as possible for a developer to write.
- __Readable__: Another developer should be able to read your code and understand what it does and how. Put comments where necessary, but implement things in an easily understandable way.
- __Maintainable__: Code should be reasonably adaptable to changes during a product's life cycle, and easy to maintain by any developer.

Striving for these aspects require balancing (example: it's often advisable to sacrifice some degree of efficiency to make code more maintainable, and vice versa).

Some advices to get good code are:

- __Use data structures generously__: 
  - Example: Write a function to add two mathematical expression of the form Ax<sup>a</sup> + Bx<sup>b</sup> + …
  - Bad implementation: Store the expression as a single array of double, where the kth element is the coeficient of the x<sup>k</sup> term. However, this doesn't support negative exponents, and requires an array of 1000 elements just to store expression x<sup>1000</sup>.
  - Less bad implementation: Store the expression in two arrays (`coefficients` and `exponents`). However this is messy: you keep track of two arrays for one expression, arrays of different lengths produce undefined values, and returning an expression is annoying because you've to return two arrays.
  - Good implementation: Design a data structure for the expression (`class ExprTerm { double coefficient; double exponent }`). Expressions can be passed as arrays. This demonstrates you think about how to design your code.

- __Appropriate code reuse__:
  - Example: Write a function to check if a binary number (string) equals an hexadecimal number (string).
  - Implemented function and reusable helper functions are:
    - `bool compareBinToHex(string, string)`
      - `int convertFromBase(string number, int base)`: Convert a given number of a given base to an integer.
	    - `int digitToValue(char c)`: Converts a digit to integer.
  - Implementing `convertFromBin` and `converFromHex` would make our code harder to write and maintain.

- __Modular__: Separate isolated chunks of code out into their own methods. This helps keep code maintainable, readable, and testable. As code gets more complex, modularity becomes increasingly important.
  - Example: Swap the minimum and maximum element in an integer array.
  - Not modular: Implement everything in `void swapMinMax(int[] array)`.
  - Modular: Implement `void swapMinMax(int[] array)`, which uses:
    - `int getMinIndex(int[] array)`
	- `int getMaxIndex(int[] array)`
	- `void swap(int[] array, int m, int n)`

- __Flexible and Robust__: Write flexible, general-purpose code, . This may require using variables instead of hard-coded values, or templates/generics. However, if the solution is too complex for the general case, and it seems unnecessary, the simple expected case may be better.
  - Example: Check if a normal tic-tac-toe board has a winner. We can assume it's a 3x3 board; or even better, implement a general way for a NxN board.

- __Error checking__: Don't make assumptions about the input. Validate that it is what is should be (through `assert` statements or if-statements). Error checking is critical in production code.
  - Example: Function `int convertFromBase(string number, int base)` can check if `base` is valid, and ensure that each digits falls within the allowable range.
  - Point out that you would write the checks. If they are complex, leave some space and indicate that you will fill them once finished with the rest of the code.


## The offer and beyond

### Handling offers and rejection

- **Offer deadline**: Offers almost always come with a deadline attached, usually of 1-4 weeks. You can ask for an extension if necessary.

- **Declining offer**: If you want to decline the offer, do it on good terms and keep a line of communication open. Provide a reason that is non-offensive and inarguable (like telling a big company that "I think a startup is the right choice for me at this time").

- **Rejection**: It doesn't mean you're not a great engineer. These interviews are not perfect and many good engineers get rejected. That's why companies often accept to re-interview previously rejected candidates, some even reach out them or expedite their application. Build a bridge to re-apply: thank your recruiter, explain that you're disappointed but that you understand their position, and ask when you can re-apply. You can also ask for feedback, though not all companies offer it.

### Evaluating the offer

Once you get an offer, the recruiter will encourage you to accept it. While evaluating the offer, you should consider:

- **Financial package**: Don't look too much at the salary. You should also look at:
  - __One time perks__ (signing bonus, relocation, …): When comparing offers, amortize this cash over 3 years (or however long you expect to stay).
  - __Cost of living difference__: Taxes and other cost of living differences can make a big difference in your take-home pay.
  - __Annual bonus__: They are 3-30% at tech companies. Your recruiter might reveal the average annual bonus, but if not, check with friends at the company.
  - __Stock options and Grants__: Equity compensation can form a big part of your annual compensation. When comparing, amortize it over 3 years and lump that value into salary.
- **Career development**: Think about how this offer would impact your career path. Consider:
  - How good does this company looks on my resume?
  - How much will I learn? Will I learn relevant things?
  - What's the promotion plan? How do developers careers progress?
  - If I want to move into management, does this company offer a realistic plan?
  - Is the company/team growing?
  - If I want to leave the company, is it near other companies I'm interested in, or will I need to move?
- **Company stability**: No one wants to be fired or laid off. The more stable companies are also often growing more slowly. The emphasis you put on company stability depends on you and your values (can you find a new job quickly? do you have work visa restrictions? …).
- **Happiness factor**: Consider how happy you will be. These factors can impact that:
  - __Product__: Many people look heavily at what product they're building. However, for most engineers, there're more important factors (who you work with …).
  - __Manager and Teammates__: This is often the reason one love or hate his job.
  - __Company culture__: It's tied to everything (how decisions get made, social atmosphere, company organization, …).
  - __Hours__: How long is the typical work day? Does it meshes with your lifestyle? Remember that hours before major deadlines are  typically much longer.
  - Note that if you're given the opportunity to switch teams easily, you could find a team and product that matches you well.

### Negotiation

The financial benefits of negotiating are usually worth it. The difference you can get from negociating is what you pay for not negociating. Tips for negociating:

- __Just do it__. Negociating is not nice, but it's so worth it. Recruiters won't revoke an offer because you negociated, so you've little to lose.
- __Have a viable alternative__. Recruiters  negociate with you because they're concerned you may not join the company otherwise, especially if you have alternative options.
- __Have a specific "Ask"__: It's more effective to ask for additional $7000 in salary than just ask for "more" (the recruiter may add $1000 and technically satisfy you).
- __Overshoot__: In negotiations, people usually don't agree to your demand. Ask for a bit more than you really want, since the company will probably meet you in the middle.
- __Think beyond salary__: Companies often prefer to negociate non-salary components (equity, signing bonus, relocation benefits in cash, …), since they could end up paying you more than your peers.
- __Use your best medium__: It's usually better to negociate over the phone. If you're not comfortable, do it via email.
- Big companies often have "levels" for employees. Employees at a particular level are paid around the same amount. You can negociate within the salary range for your level, but going beyond requires to convince the recruiter and your future team that your experience matches a higher level (difficult, but feasible).

### On the job

Once you join the company, think about your career path.

- __Set a timeline__: Avoid falling into a complacency trap where you stay in a position that doesn't advance your career (neither your skill set nor your resume are improved). Outline your career path (Where will you go in 10 years, and how will you get there?), and each year think about how your skill set advanced the past year and what will you get the next year.
- __Build strong relationships__: Applying online is tricky; a personal referral is much better, and your ability to do so hingers on your network. Establish strong relationships with your manager and teammates. Keep it touch with employees that leave (example: a friendly note a few weeks after their departure). Help others, and they'll be likely to help you.
- __Ask for what you want__: Tell your manager about your goals and what you want to work on. It's up to you to pursue the challenges that help your career.
- __Keep interviewing__: Set a goal of interviewing at least once a year, even if you're not actively looking for job. This will keep your interview skills fresh, and keep you in tune with the market opportunities and salaries. You don't have to accept any offer, but it will build a connection with that company in case you join them in the future.


## Interview questions


## Arrays and Strings

Array questions and strings questions are often interchangeable (questions that use an array may be asked using a string, and vice versa).

Main C++ string types:

- **String literal** ("hi"): Type `const char[N]`. Static storage duration.
- **Array of chars** (`char buf[64]`)
- **C-style strings** (`char*`, `const char*`) (`const char* s = "hi"`): Pointer to a `\0`-terminated character array.
- **std::array** (`std::array<char, 64>`)
- **std::string** (`std::string s = "hi"`). There're variations (`std::wstring`, `std::u8string`, `std::u16string`, `std::u32string`). Efficient concatenation.
- **std::ostringstream** (`oss << x << y`): Construction helper, not true string. Builds string via streaming. Inefficient for heavy concatenation (`std::string` preferred). Produces `std::string`.

### Hash tables

**Hash tables** (`std::unordered_map`): Data structure that maps keys to values for highly efficient lookup. This can be implemented in different ways.

One common implementation is:

- This requires an __array of linked list__ and a __hash code function__.
- Insert a key-value pair:
  - Compute hash code from the key. Hash code is usually `int` or `long`. Two different keys could have same hash code (there's a finite number of ints, but an almost infinite number of keys).
  - Map the hash code to an index in the array (`hash(key) % array_length`. Two different hash codes could map to same index.
  - Store key-value pair in this index, which is a linked-list because of collisions (two different keys can have same hash code, or two different hash codes can map to same index).
- Retrieve value by its key:
  - Compute hash code from the key.
  - Compute index from the hash code.
  - Search through the linked list for the value with this key.

If there's a high number of collisions, the lookup worst runtime is O(n) (n = number of keys). We generally assume a good implementation that keeps collisions to a minimum, so it's O(1).

Another implementation uses a balanced binary search tree. This gives O(log n) lookup time, but uses less space (no need to allocate a large array), and allows to iterate through keys in order.

### Dynamic arrays

**Arrays** have fixed size, defined at construction (some languages automatically resize arrays).

**Dynamic array** is a resizable array.

**`std::vector`** (or `ArrayList` in Java) is an array that dynamically resizes itself as needed while still providing O(1) access. Typically, when the array is full, the array doubles in size (resizing factor = 2). Each doubling takes O(n) time, but happens so rarely that its amortized insertion time is still O(1).

- Why amortized insertion runtime is O(1)?
  - How many elements we copy at each capacity increase?
    - final capacity increase = n/2 elements to copy
    - previous increase = n/4
    - previous increase = n/8
    - …
    - second increase = 2
    - first increase = 1
  - Total number of copies = n/2 + n/4 + n/8 + … + 2 + 1 = less than n
  - Thus, inserting n elements takes O(n) total time. Each insertion is O(1) on average, even though some insertions take O(n) time in the worst case.

### Dynamic strings

```
string joinWords(string words[])   // Concatenate a list of strings
{
  string sentence = "";
  for (string w : words) sentence += w;
  return sentence;
}
```

In **Java**, strings are immutable, so **string concatenation** (`myString += word`) makes the string allocate a new buffer, copy the old content, and append the new part. On each concatenation, a new copy of the string is created, and it's copied over, character by character. The first iteration copies x characters, the second copies 2x, the third 3x, and so on.

- Total time  =  O(x + 2x + 3x + … + nx)  =  O(x (1 + 2 + 3 + … + n))
- 1 + 2 + 3 + … + n  =  n (n + 1) / 2
- Total time  =  O(x n<sup>2</sup>)

This is solved using the **`StringBuilder`** class. It's a mutable, efficient string-building type that allows to build up a string piece-by-piece without repeatedly creating new string objects. Similar to a `std::vector`, but for strings. This avoids the concatenation problem by creating a resizable array of all the strings, copying them back to a string only when necessary. Runtime = O(n).

```
String joinWords(string words[])
{
  StringBuilder sentence = new StringBuilder();
  for(string w : words) sentence.append(w);
  return sentence.toString();
}
```

In **C++** `std::string`s aren't immutable, so string concatenation can be performed efficiently, like a `std::vector` or `StringBuilder`. Reallocation (allocate new buffer, copy old content, and append the new part) is only done when the string capacity is not enough. Some C++ options:

- `myString = a + b + c`: Can be inefficient, potentially O(n<sup>2</sup>). It allocates temp for `a + b`, copy `a`, copy `b`, allocate temp for `(a + b) + c`, and copies again.
- Efficient appends (O(n) at most): Appends in place when capacity is sufficient. No temps.
  - `myString += word`
  - `std::string::append()`
  - `std::string::push_back()`
- **`std::string::reserve()`** can be used to preallocate space, avoiding repeated memory allocations during appending.
- **`std::ostringstream`**: It buffers internally and is efficient for many small appends.

```
#include <sstream>

std::ostringstream sb;
sb << "abc";
sb << 123;
sb << "def";
std::string result = sb.str();
size_t size = result.tellp();
```

```
std::string sb;
sb.reserve(1000);
for(int i = 0; i < 1000; ++i)
sb.append(std::to_string(i));
```

It's a good exercise to implement your own `DynamicArray` (`Vector`), `DynamicString`, and `HashTable`.

Read more: Hash table collision resolution, Rabin-Karp substring search.


## Linked lists

**Linked list:** Data structure representing a sequence of nodes. __Random access__ takes no constant time (unlike arrays) because it requires iterating. But __adding/removing__ elements from the extremes takes constant time.

- **Singly linked list:** Each node points to the next node.
- **Doubly linked list:** Each node points to the next and previous node.
  
Ways of accessing a linked list:

- __Reference to head `Node`__. Be careful when changing the head of the linked list, maybe some objects that need a reference to it might still point to the old head.
- __Class wrapping the `Node` class__. It may have a single member variable, the `Node`. This solves the previous issue.
  
__Delete node__: In singly linked lists, given node `n`, find `prev` and set `prev.next = n.next`. In double linked lists, we must also set `n.next.prev = n.prev`. Check for null pointer. Update the head or tail pointer as necessary. Consider if a removed node should be deallocated (`delete`) (memory management).
  
**"Runner" (or second pointer) technique:** Iteration through the linked list with 2 pointers simultaneously, one ahead of the other. The "fast" node might be ahead by a fixed amount, or might be hopping multiple nodes for each one node that the "slow" node iterates through.

Example: Given linked list a<sub>1</sub>→a<sub>2</sub>→…→a<sub>n</sub>→b<sub>1</sub>→b<sub>2</sub>→…→b<sub>n</sub>, rearrange it into a<sub>1</sub>→b<sub>1</sub>→a<sub>2</sub>→b<sub>2</sub>→…→a<sub>n</sub>→b<sub>n</sub>. The length of the linked list is unknown, but we know it's an even number.

1. Locate the middle: p1 (fast pointer) moves every 2 elements for every one move tha p2 makes. When p1 hits the end of the linked list, p2 will be at the midpoint.
2. Rearrange nodes: Move p1 back to the front and iterate again with both pointers. On each iteration, p2 selects an element and inserts it after p1.

**Recursive problems:** Some linked list problems rely on recursion. If you have trouble solving a linked list problem, explore if a recursive approach works. Recursive algorithms take at least O(n) space (n = depth of the recursive call). All recursive algorithms can be implemented iteratively, although they may be much more complex. Recursive solutions are often cleaner but less optimal.


## Stacks and Queues

Stacks and Queues can be implemented as arrays or linked-lists.

### Stack

A **stack** implements LIFO (Last-In First-Out) ordering. It doesn't offer constant-time access to the ith item, but allows constant-time addition and removal on top (no need of shifting elements around). Operations:

- `pop()`: Remove top item.
- `push(item)`: Add item to the top.
- `top()`: Return top.
- `empty()`: Return true if it's empty.

Stacks can be useful in certain recursive algorithms. Examples:

- To push temporary data onto a stack as you recurse, and remove them as you backtrack (for example, because the recursive check failed).
- To implement a recursive algorithm iteratively.

### Queues

A **queue** implements FIFO (First-In First-Out) ordering. Operations:

- `pop()`: Remove first item.
- `push(item)`: Add item at the end.
- `front()`: Return first item.
- `empty()`: Return true if it's empty.

Queues are often used in:

- Breadth-first search. Example: to use a queue to store a list of nodes to process. Each time we process a node, we add its adjacent nodes to the back of the queue. This way, nodes are processed in the order in which they're viewed.
- Implementing a cache.


## Trees and Graphs

### Trees

Operations on trees are usually more complicated than in linear structures (arrays, linked lists…), and the worst case and average case time may vary wildly.

**Tree:** Data structure composed of nodes. Each tree has a root node, which can have zero or more child nodes. Each child has zero or more childs, and so on. A tree cannot contain cycles. The nodes may or may not be in a particular order, they can have any data type as values, and they may or may not have links back to their parent nodes.

We typically don't use a `Tree` class in interview questions. It can be used if it's good for your code, but it rarely is.

```
class TreeNode
{
public:
  string name;
  TreeNode* child_1;
  TreeNode* child_2;  
}
```

**Leaf node:** Node with no children.

**Tree types:** There're different types, based on different characteristics.

- **Number of nodes:**
  - **Binary tree:** Nodes have up to 2 children. 
  - **Ternary tree:** Nodes have up to 3 children.
  - **Quaternary tree (or Quadtree):** Nodes have up to 4 children (quad nodes).
  - **X-ary tree:** Nodes have up to X children (example: 10-ary tree).
  
- **Nodes order:**
  - **Binary search tree (BST):** Every node fits a specific ordering property (`all_left_descendants <= n < all_right_descendents`). This must be true for each node n. Depending on the definition used, it may or may not allow duplicate values, or store duplicates on the left, right, or either side.
  - **Non binary search tree:** No ordering.

- **Balancing:**
  - **Unbalanced:** Imbalanced tree.
  - **Balanced:** Tree not terribly imbalanced. It's balanced enough to ensure O(log n) time for `insert` and `find`. Examples: red-black tree, AVL tree.

- **Special binary trees:**
  - **Complete:** Every tree level is fully filled, except for perhaps the last level. The last level is filled left to right.
  - **Full:** Every node has either 0 or 2 children.
  - **Perfect:** Tree that is both full and complete, where all leaf nodes are at the same level (so the last level has the maximum number of nodes). It has exactly 2<sup>k</sup>-1 nodes (k = number of levels). This tree is rare.
  
**Binary tree traversal:**

- **In-order:** First visit left branch, then current node, then right branch. In a BST, it visits nodes in ascending order. Most common traversal type.
- **Pre-order:** First visit current node before its child nodes. Root is the first node visited.
- **Post-order:** First visit child nodes before root. Root is the last node visited.

```
void inOrderTraversal(TreeNode* node)
{
  if(!node) return;
  inOrderTraversal(node->left);
  visit(node);
  inOrderTraversal(node->right);
}

void preOrderTraversal(TreeNode* node)
{
  if(!node) return;
  visit(node);
  preOrderTraversal(node->left);
  preOrderTraversal(node->right);
}

void postOrderTraversal(TreeNode* node)
{
  if(!node) return;
  postOrderTraversal(node->left);
  postOrderTraversal(node->right);
  visit(node);
}
```

### Binary heaps

**Binary heap**: Data structure that stores values and allow to retrieve the minimum (or maximum) value in just O(log n) time. Implemented as an array (to make it easy to find the bottom rightmost spot. Two types:

- **Min-heap:** Complete binary tree where each node is smaller than its children (ascending order). Thus, the root is the minimum element in the tree. Key operations: `insert` and `extract_min`.
- **Max-heap**: Similar to min-heap, but elements are in descending order. Key operations: `insert` and `extract_max`.

**Key operations** for min-heap:

- **`insert`** (O(log n)): Start inserting the element at the bottom, at the rightmost spot (to maintain the complete tree property). Then, swap it with its parent until the min-heap property is restored (where element > parent) (bubble up).
- **`extract_min`** (O(log n)): The minimum element is at the top. We replace it with the last element (bottommost, rightmost element) and swap it with the smaller children until the min-heap property is restored (bubble down).

Max-heap operations are similar, but maintaining max-heap properties.

### Tries (Prefix trees)

**Trie**: Variant of an n-ary tree in which characters are stored at each node. Each path down the tree may represent a word. A complete word can be indicated using a null node (implemented as a special type of child that inherits from `TrieNode`) or a `bool` flag in the "parent" node.

If a null node is used, a node can have anywhere from 1 through ALPHABET_SIZE + 1 children, or 0 through ALPHABET_SIZE if a `bool` flag is used.

![trie](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/coding_1.png)

A trie is used to store an entire language for quick prefix lookups. It can check if a string is a valid prefix in O(K) time (K = length of string). Tries can optimize many problems involving lists of valid words.

A hash table can quickly look up whether a string is a valid word, but it cannot tell if a string is a prefix of any valid word, unlike a trie. We often consider that hash tables take O(1) for lookup, but they actually take O(K) because it has to read all characters in the input.

### Graphs

**Graph**: Collection of nodes with edges between (some of) them. It can be either directed (one-way street edges) or undirected (two-way street edges). It might consist of multiple isolated subgraphs. It can have cycles.

- **Connected graph**: Graph where there is a path between every pair of vertices.
- **Acyclic graph**: Graph without cycles.
- **Tree**: Connected and acyclic graph. A tree is a type of graph, but not all graphs are trees. 

![graph](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/coding_2.png)

There're two common ways to represent a graph: __Adjacency list__ and __Adjacency matrices__.

**Adjacency list** (AL): Most common representation. Every vertex (or node) stores a list of adjacent vertices.

- Example: In an undirected graph, an edge like (a, b) would be stored twice (once in a's adjacent vertices and once in b's adjacent vertices.

- Implementation 1: It could look essentially the same as a tree node. A `Graph` class is used because, unlike a tree, you can't necessarily reach all nodes from a single node.

```
class Graph {
  public:
  vector<Node*> allNodes;
};

class Node {
  public:
  string name;
  vector<Node*> children;
}
```

- Implementation 2: An array (or hash table) of lists (arrays, vectors, linked lists…) can store the adjacency list (example: `{ {1}, {2}, {0, 3}, {2}, {6}, {4}, {5} }`). This is more compact but isn't quite as clean, so we tend to use node classes.

**Adjacency matrices** (AM): NxN boolean matrix (N = number of nodes). A `true` value at `matrix[i][j]` indicates an edge from node `i` to node `j`. In an undirected graph, an adjacency matrix will be symmetric. In a directed graph it won't (necessarilly) be.

- The same graph algorithms used on ALs can be performed with AMs, but they may be somewhat less efficient. In ALs you can easily iterate through the neighbors of a node, but in AMs you need iterate through all nodes to identify a node's neighbors.

![adjacency matrix](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/coding_3.png)

**Graph search**: The two more common ways to search a graph are __depth-first search__ and __breadth-first search__.  We mark visited nodes as "visited" to avoid cycles.

- **Depth-first search (DFS)**: Start at the root (or any other node) and explore each branch (neighbor) completely before moving on to the next branch. We go deep first before we go wide. Pre-order and other forms of tree traversal are a form of DFS, but for a graph we have to check if the node has been visited (otherwise, we can get stucked in an infinite loop). It often uses recursion.

```
void search(Node* root)
{
  if (root == nullptr) return;
  visit(root);
  root.visited = true;
  for (Node* n : root.adjacent)
    if (n.visited == false)
	  search(n);
}
```

- **Breath-first search (BFS)**: Start at the root (or any other node) and explore each neighbor before going on to any of their children (search level by level out from first node). We go wide before we go deep. An iterative solution (no recursion) involving a queue usually works best.

```
void search (Node* root)
{
  Queue<Node*> queue;
  root->marked = true;
  queue.enqueue(root);
  
  while (!queue.empty())
  {
    Node r = queue.dequeue();
	visit(r);
	for (Node* n : r.adjacent)
	  if (n.marked == false)
	  {
	    n.marked = true;
		queue.enqueue(n);
	  }
  }
}
```

![graph search](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/coding_4.png)

DFS and BFS tend to be used in different scenarios:

- Visit every node in the graph: DFS is often preferred since it's a bit simpler.
- Find shortest path (or any path) between two nodes: BFS is generally better. DFS may take a long time, and won't find the shortest path. BFS keeps you close to the first node for as long as possible, while DFS goes far away and back many times.

**Bidirectional search**: Used to find the shortest path between two nodes. Two BFSs run simultaneously, one from each node. When their searches collide, we have found a path. This is faster than a single BFS because:

- Consider a graph where every node has at most k adjacent nodes and the shortest path from node a to node b has lenght d.
- BFS would search through d levels (k<sup>d</sup> nodes), which takes O(k<sup>d</sup>) time.
- Bidirectional search has two searches where each one visits ~d/2 levels (~2·k<sup>d/2</sup> nodes in total) (the path's midpoint), which takes O(k<sup>d/2</sup>) time.
- Bidirectional search is faster by a factor of k<sup>d/2</sup> (because (k<sup>d/2</sup>)·(k<sup>d/2</sup>) = k<sup>d</sup>).

Additional reading: Topological sort, Dijkstra's algorithm, AVL trees, Red-black trees.


## Bit manipulation

### Basics

**Addition** rules: Same as decimal additions, but 1 + 1 equals 0 and carries 1.

- Examples:  1 + 1 = 10;  1 + 1 + 1 = 11

```
  1011
+ 1101
------
 11000
```

**Subtraction** rules: Same as decimal subtractions, but 0 - 1 borrows from next bit and equals 1.

```
  1010
- 0111
------
  0011
```
  
**Multiplication** rules: Same as decimal multiplications.

```
   101
x   11
------
   101
+ 101
------
  1111
```

**Division** rules: Same as decimal divisions (divide using subtraction, shift the divisor as needed, and bring down bits sequentially).

```
 1101 / 11
-11     100
-----
 0001
```

**Shifting**: Given a number (`0101`), we can shift al digits left (`1010`) or right (`0010`). Left shifting (`<<`) N times is equivalent to multiplying by 2<sup>N</sup> times. Similarly, right shifting (`>>`) is equivalent to dividing.

Operators:

- `~` (NOT): Not true
- `^` (XOR): Only one true
- `&` (AND): Both true
- `|` (OR): At least one true

### Manual examples

- `0110 + 0010` = `1000`
- `0011 + 0010` = `0101`
- `0110 - 0011` = `0011`
- `1000 - 0110` = `0010`
- `0011 * 0101` = `1111`
- `0011 * 0011` = `1001`
- `1101 >> 2` = `0011`
- `1101 ^ 0101` = `1000`
- `0110 + 0110` = `1100`   (this is equivalent to 0110 * 2, which is equivalent to shifting 0110 left by 1)
- `0100 * 0011` = `1100`   (0100 equals 4, and multiplying by 4 is left shifting by 2)
- `1101 ^ (~1101)` = `1111`   (think bit by bit. If you XOR a bit with its own negated value, you always get 1)
- `1011 & (~0 << 2)` = `1000`   (~0 is a sequence of 1s, and ~0 << 2 is 1s followed by two 0s. ANDing this with another value clears the last two bits of the value)

**Bit facts and tricks**: These operations occur bit-by-bit. What happens in one bit never impacts the others. Thus, if these operations are true for a single bit, then they're true for a sequence of bits. A sequence of identical bits are represented as 1s or 0s.

- x ^ 0s = x
- x ^ 1s = ~x
- x ^ x = 0
- x & 0s = 0
- x & 1s = x
- x & x = x
- x | 0s = x
- x | 1s = 1s
- x | x = x

**Two's complement and Negative numbers**:

"Two's complement" has two meanings:

- Binary representation system used to encode signed integers. 
- Standard method used by modern computers to represent negative numbers. This allows efficient arithmetic operations using the same hardware as unsigned binary, simplifying circuit design.

Key features:

- The most significant bit (MSB) acts as **sign bit**: 1 (positive or zero), 0 (negative).
- A positive number is represented as its standard binary form.
- A negative number is represented as the **two's complement of its absolute value** (with sign bit = 1).

Negative value representation (different views):

- Two's complement of an N-bit number = Complement of the number with respect to 2<sup>N</sup> (N: number of bits used for the number, excluding the sign bit).

  - Example: The 4-bit signed integer -3 is represented as the two's complement of 3 (`011`) with respect to 2<sup>3</sup>, which equals to 5 (`101`), with the signed bit (`1101`).

- -K as an N-bit binary number = `concat(1, 2<sup>N-1</sup> - K)`.

- Invert the bits in the positive representation and add 1.

  - Example: Take 3 (`011`), flip the bits (`100`), add 1 (`101`), and prepend the sign bit (`1101`).

Example of 4-bit integers: Observe that the values at each side are identical, and that the absolute values of both sum 2<sup>3</sup>.

| Positives  |  Negatives  |
|:----------:|:-----------:|
| 0: `0 000` |             |
| 1: `0 001` | -7: `1 001` |
| 2: `0 010` | -6: `1 010` |
| 3: `0 011` | -5: `1 011` |
| 4: `0 100` | -4: `1 100` |
| 5: `0 101` | -3: `1 101` |
| 6: `0 110` | -2: `1 110` |
| 7: `0 111` | -1: `1 111` |

**Right shift**: This operator can be:

- __Logical__: Just shift all the bits. Example: `10110101` (-75) → `01011010` (90). The sign bit gets a 0. Shifting repeatedly results in a sequence of 0s (`00000000`).
- __Arithmetic__: Roughly divides by 2. Example: `10110101` (-75) → `11011010` (-38). This preserves the sign bit, and shifts it to the most significant bit. Shifting repeatedly results in a sequence of 1s (`11111111`), which for a signed integer is -1.

In C++, for signed integers, right shift is implementation-defined, not undefined. But in practice, all mainstream compilers on two’s-complement machines perform an arithmetic shift.

```
unsigned int x = 0b0100;   // 4
unsigned int y = x >> 2;  // 0b0001 (1)
```

__Bit mask__: Value used in bitwise operations (select, set, clear, test) to operate on specific bits in another value. It works by applying operations (like `&`, `|`, or `^`) so that only the bits of interest are affected, while the others remain unchanged. Common types of masks are:

- Single-bit mask (`00010000`): Shift 1 over by `i` bits (`1 << i`).
- Inverted mask (`11101111`): Shift 1 over by `i` bits and negate it (`~(1 << steps)`).
- Composite (`10010111`)
- Field (`00111100`)
- 0s (`00000000`): Sequence of zeros (`0`).
- 1s (`11111111`): Sequence of ones (`~0` or `-1`).

**Common bit tasks**:

- __Get bit__: Get single-bit mask and perform `number AND mask`. This clears all bits other than the bit at position i.

```
bool getBit(int number, int i) {
  return ((number & (1 << i)) != 0);
}
```

- __Set bit__: Get single-bit mask and perform `number OR mask`. Only the value at position i will change.

```
int setBit (int number, int i) {
  return number | (1 << i);
}
```

- __Clear bit__: Get inverted mask and perform `number AND mask`. Only the ith bit will be cleared.

```
int clearBit(int number, int i) {
  return num & (~(1 << i));
}
```

  - __Clear all bits from the most significant bit through i (inclusive)__: Get single-bit mask (`00010000`), subtract 1 from it (this gets a sequence of 0s followed by i 1s) (`00001111`), and perform `number AND mask`. This leaves just the last i bits.
  
```
int clearBitsMSBthroughI(int number, int i) {
  return number & ((1 << i) - 1);
}
```

  - __Clear all bits from i through 0 (inclusive)__: Take a sequence of 1s (which is -1) and shift it left by i + 1 bits (`11110000`) (this gets a sequence of 1s followed by i 0 bits). Performing `number AND mask` leaves just the first i bits.

```
int clearBitsIthrough0(int number, int i) {
  return number & (-1 << (i + 1));
}
```

- __Update bit__ (set ith bit to a value v): Clear bit at position i using an inverted mask. Create a mask by shifting the intended value v left by i bits (creates number with bit i = v and all other bits = 0). Perform `number OR mask` to update the ith bit (only happens if v = 1).

```
int updateBit(int number, int i, bool bitValue) {
  int value = bitValue ? 1 : 0;
  int mask = ~(1 << i);
  return (num & mask) | (value << i);
}
```

In a few words:

- __Get bit__: Single-bit mask + `AND`
- __Set bit__: Single-bit mask + `OR`
- __Clear bit__: Inverted mask + `AND`
  - __Clear [N, i]__: Single-bit mask - 1 + `AND`
  - __Clear [i, 0]__: 1s shifted left + `AND`
- __Update bit__: Clear bit i. Single-bit mask with desired value + `OR`

In many bit manipulation problems it's very easy to wind up with off-by-one errors, so test your code.


## Math and Logic puzzles

Many companies don't like puzzles. However, they may ask a reasonable fair one (no wording tricks) that can almost always be logically deduced. Many puzzles have their foundations in mathematics or computer science. Interviewers want to see how you tackle a problem, so talk and show how you approach it.

### Prime numbers

**Fundamental theorem of Arithmetic (FTA):** Every positive integer greater than 1 can be un iquely expressed as a product of prime numbers.

- Example: 84 = 2<sup>2</sup> * 3<sup>1</sup> * 5<sup>0</sup> * 7<sup>1</sup> * 11<sup>0</sup> * 13<sup>0</sup> * 17<sup>0</sup> * … (note that many of these primes have an exponent of zero)

**Divisibility:** The FTA means that, in order for a number x to divide a number y (x\y, or mod(y,x)=0), all primes in x's prime factorization must be in y's prime factorization.

- Example:
  - x = 2<sup>j0</sup> * 3<sup>j1</sup> * 5<sup>j2</sup> * 7<sup>j3</sup> * 11<sup>j4</sup> * …
  - y = 2<sup>k0</sup> * 3<sup>k1</sup> * 5<sup>k2</sup> * 7<sup>k3</sup> * 11<sup>k4</sup> * …
  - If x\y, then for all i, ji <= ki
- Greatest common divisor of x and y:
  - gcd(x,y) = 2<sup>min(j0,k0)</sup> * 3<sup>min(j1,k1)</sup> * 5<sup>min(j2,k2)</sup> * …
- Least common multiple of x and y:
  - lcm(x,y) = 2<sup>max(j0,k0)</sup> * 3<sup>max(j1,k1)</sup> * 5<sup>max(j2,k2)</sup> * …
- Fun exercise: gcd * lcm
  - = 2<sup>min(j0,k0)</sup> * 2<sup>max(j0,k0)</sup> * 3<sup>min(j1,k1)</sup> * 3<sup>max(j1,k1)</sup> * …
  - = 2<sup>min(j0,k0) + max(j0,k0)</sup> * 3<sup>min(j1,k1) + max(j1,k1)</sup> * …
  - = 2<sup>j0 + k0</sup> * 3<sup>j1 + k1</sup> * …
  - = 2<sup>j0</sup> * 2<sup>k0</sup> * 3<sup>j1</sup> * 3<sup>k1</sup> * …
  - = x * y
  
**Checking for primality:**

- Solution 1 (naive): Iterate form 2 through n-1, checking for divisibility on each iteration.

```
bool prime(int n)
{
  if (n < 2) return false;
  
  for (int i = 2; i < n; i++)
    if (n % i == 0) return false;
	
  return true;
}
```

- Solution 2 (improved): Iterate only up through √n.
  - For every number a which divides n evenly, there's a complement b, where a * b = n.
  - If a > √n, then b < √n (since (√n)<sup>2</sup> = n).
  - Thus, we don't need a to check n's primality, since we would have already checked with b.

```
bool prime(int n)
{
  if (n < 2) return false;
  
  int sqrt = (int)std::sqrt(n);
  
  for (int i = 2; i <= sqrt; i++)
    if (n % i == 0) return false;
	
  return true;
}
```

- Solution 3 (best): Check only if n is divisible by a prime number.
  - Sieve of Eratosthenes: Highly efficient way to generate a list of primes. All non-prime numbers are divisible by a prime number. Given a list of all numbers up through a value `max`. First, cross off all numbers divisible by 2. Then, look for the next prime (next non-crossed off number) and cross of all numbers divisble by it (2, 3, 5, 7, 11…). This way, we wind up with a list of prime numbers from 2 through `max`.

```
std::vector<bool> sieveOfEratosthenes(int max)
{
  std::vector<bool> flags(max + 1, true);
  int count = 0;
  int prime = 2;
  
  flags[0] = false;
  flags[1] = false;
  
  while (prime <= std::sqrt(max))
  {
    crossOff(flags, prime);   // Cross off remaining multiples of prime
	prime = getNextPrime(flags, prime);
  }
  return flags;
}

int getNextPrime(std::vector<int>& flags, int prime)   // Cross of remaining multiples of prime
{
  for (int i = prime * prime; i < flags.length(); i += prime)
    flags[i] = false;
}

int getNextPrime(std::vector<bool>& flags, int prime)
{
  int next = prime + 1;
  while (next < flags.length() && !flags[next])
    next++;

  return next;
}
```

This code can be optimized. Example: Only use odd numbers in `flags`.

### Probability

Probabilities can be represented with a Venn diagram: Given 2 areas, A and B, representing the relative probability of 2 events, the overlapping area is the event `{A and B}` (A&xcap;B). 

**Probability of A and B**: P(A and B) = P(B given A) P(A) = P(A given B) P(B)

- P(B given A): Percent of A that is B. P(B) given P(A) = 1.
- Example: Consider 10 unique numbers in range [1, 10]
  - P(x is even) = 0.5
  - P(x <= 5) = 0.5
  - P(x is even and x <= 5)  =  P(x is even given x <= 5) P(x <= 5)  =  (2/5) * (1/2)  =  1/5
- Bayes' Theorem: P(A given B) = P(B given A) P(A) / P(B)

**Probability of A or B**: P(A or B) = P(A) + P(B) - P(A and B)

- Example: Consider 10 unique numbers in range [1, 10]
  - P(x is even or x <= 5)  =  P(x is even) + P(x <= 5) - P(x is even and x <= 5)  =  (1/2) + (1/2) - (1/5)  =  4/5

**Independence**: Given A and B, one happening tells nothing about the other happening.

- P(A and B) = P(A) P(B)
- P(B given A) = P(B)

**Mutual exclusivity**: Given A and B, if one happens, then the other cannot happen.

- P(A and B) = 0
- P(A or B)  =  P(A) + P(B) - 0  =  P(A) + P(B)

Two events cannot be both independent and mutually exclusive, except when both have probability zero.

### Develop rules and patterns

You should write down "rules" or patterns that you discover while solving a problem. This helps remember them and make the problem easier.

Example: Given 2 ropes that take each one hour to burn, how would you use them to time exactly 15 minutes? The ropes have uneven densities, so half the rope length-wise doesn't necessarily take half an hour to burn.

- We have rope X that takes x minutes to burn, and rope Y that takes y minutes.
- Rule 1: Given X and Y, we can time x+y minutes.
- Rule 2: Given X, we can time x/2 minutes by lighting it at both ends.
- Rule 3: We can turn rope Y into a rope that takes y-x minutes or y-(x/2) minutes.
- Thus, we can turn one rope into a 30 minutes rope. If we thenlight it on the other end, it will be done after 15 minutes.
- Steps: Light rope 1 at both ends, and rope 2 at one. When rope 1 is consumed (30 min), light rope 2 at the other end. In 15 minutes rope 2 will be consumed.

### Worst case shifting

Many puzzles are worst-case minimization problems (like minimizing an action, or doing something at most a specific number of times). A useful technique is trying to "balance" the worst case: if an early decision results in a skewing of the worst case, we can sometimes change the decision to balance the worst case.

Example: You have 9 balls, where all weight the same except one that is heavier, and a balance that only tells which side (right or left) is heavier. Find the heavy ball in just two uses of the scale.

- Dividing the balls in sets of 4 requires 3 weighings (one too many).
  - Imbalance: The 9th ball takes 1 weighing to discover if it's heavy, whereas the others take 3.
  - Worst case balancing: "Penalizing" the 9th ball by putting more balls off to the side lightens the load on the others.
- Dividing the balls in sets of 3 requires 2 weighings.
  - After one measure we know which set has the heavy ball. Repeating this step we find the heavy ball.

### Algorithm approaches

Puzzles are often algorithm questions without technical aspects. If you're stuck, consider applying one of the approaches for solving algorithm questions (see [optimize & solve techniques](#optimize-&-solve-technique-BUD-bottlenecks-unnecessary-work-duplicated-work)):

- **BUD** (Bottlenecks, Unnecessary work, Duplicated work)
- **DIY** (Do It Yourself)
- **Simplify and Generalize**
- **Base case and Build**
- **Data structure brainstorm**

Additional reading: [Useful math](#useful-math)


## Object oriented design

OOD questions require sketching out the classes and methods to implement technical problems or real-life objects. This shows your coding style and how you create elegant, maintainable object-oriented code.

### Approach

This approach works well for many problems:

- **Handle ambiguity**: OOD questions are often intentionally vague in order to test whether you'll make assumptions or ask clarifying questions. You should inquire Who and How is going to use it. Depending on the question, you may want to ask the "six Ws" (Who, What, Where, When, How, Why). When describing the OOD of a coffe maker, we need to know whether it's an industrial machine for a massive restaurant or a simple machine used by the elderly for just black coffee.

- **Define the core objects**: For a `Restaurant`, they might be things like `Table`, `Guest`, `Party`, `Order`, `Meal`, `Employee`, `Server`, and `Host`.

- **Analyze relationships** between the objects: Which objects are members of which other objects? Do any objects inherit from any others? Are relationships many-to-many or one-to-many? You can often make incorrect assumptions, so you should ask how general purpose your design should be.

  - Example: `Party` should have an array of `Guests`. `Server` and `Host` inherit from `Employee`. Each `Table` has one `Party`, but each `Party` may have multiple `Tables`. There's one `Host` for the `Restaurant`.

- **Investigate actions**: Consider the key actions that the objects will take and how they relate to each other. You may find that you forgot some objects, and you'll need to update your design.

  - Example: A `Party` walks into the `Restaurant`, and a `Guest` requests a `Table` from the `Host`. The `Host` looks up the `Reservation` and, if it exists, assigns the `Party` to a `Table`. Otherwise, the `Party` is added to the end of the list. When a `Party` leaves, the `Table` is freed and assigned to a new `Party` in the list.
  
### Design patterns

Interviewers often try to test your capabilities, not your knowledge. However, the **Singleton** and **Factory Method** design patterns are widely used in interviews. Study design patterns to improve your software engineering skills. You should create a design that works for the problem; sometimes it might be an established pattern, but in many other cases it's not.

- **Singleton class**: It ensures that a class has only one instance and ensures access to the instance through the application. Useful for "global" objects with exactly one instance (we might want `Restaurant` to be a singleton). Many people dislike it (one reason is that it can interfere with unit testing).

```
class Restaurant
{
protected:
  Restaurant() {...}
  static Restaurant* _instance = nullptr;

public:
  Restaurant* getInstance()
  {
    if (!_instance)
	  _instance = new Restaurant();
	return _instance;
  }
}
```

- **Factory Method**: It offers an interface for creating an instance of a class, with its subclasses deciding which class to instantiate. Two possible implementations:

  - Creator class is abstract and doesn't provide an implementation for the Factory Method.
  - Creator class is concrete and provides an implementation of the Factory Method (which would take a parameter representing which class to instantiate).

```
class CardGame
{
public:
  static CardGame* createCardGame(GameType type)
  {
    if (type == GameType::Poker)
	  return new PokerGame();
	else if (type == GameType::BlackJack)
	  return new BlackJackGame();
	
	return nullptr;
  }
}
```


## Recursion and Dynamic programming

People typically have 50% accuracy in their "this sounds like a recursive problem" instinct. Many recursive problems follow a similar pattern. A good hint that a problem is recursive is that it can be built off of subproblems. Problems beginning with the following statements are often, but not always, good candidates for recursion:

- Design and algorithm to compute the nth…
- Write code to list the first n…
- Implement a method to compute all…

### Recursive approach

Recursive solutions are built off of solutions to subproblems. The most common approaches to develop them are:

- **Bottom-Up**: First, know how to solve the problem for a simple case (like a one-element list). Then figure out how to solve it for 2 elements, then for 3, and so on. Think about how to build the solution for one case off of the previous case (or cases).

- **Top-Down**: Think about how to divide the problem for case N into subproblems. Be careful of overlap between the cases.

- **Half-and-Half**: Divide the data set in half. Examples: binary search and Merge sort.

**Additional notes:**

Recursive solutions are often cleaner but less optimal.

**Parts** of a recursive function:

```
int fact(int n)
{
  if (!n) return 1;
  return n * fact(n - 1);
}
```

- __Base case__ (`if (!n) return 1`): Prevents infinite recursion.
- __Recursive case__ (`fact(n - 1)`): The function calls itself with a smaller/simpler input version.
- __Progress toward base case__ (`n - 1`): Each recursive call reduce problem size or move closer to termination.

**Types** of recursive functions:

- __Direct vs. Indirect__ recursion:
  - __Direct__: Function calls itself directly.
  - __Indirect__: Function calls another function that calls the first.

- __Tail vs. Non-tail__ recursion:
  - __Tail__: The recursive call is the last operation in the function. Compilers can optimize it into a loop.
  - __Non-tail__: The recursive call must be combined with other work.
  
- __Linear__ recursion: Each call makes at most one recursive call (factorial, Fibonacci, binary search…).

- __Tree__ recursion: Each call makes more than one recursive call (naive Fibonacci…), expanding into a recursion tree.

- __Divide & Conquer__ recursion: Problem is divided into independent subproblems, solved recursively, then combined (merge sort, quicksort, binary search…).

- __Mutual__ recursion (subset of indirect recursion): Two or more functions call each other in turns (determining if a number is even/odd…).

```
bool isEven(int n) { return !n || isOdd (n - 1); }
bool isOdd (int n) { return  n && isEven(n - 1); }
```

**Building intuition**:

- __Break down__ problems into smaller subproblems:
  - __Base case__: Simplest problem version where recursion stops.
  - __Recursive case__: Small problem instance close to the base case.
- __Recursive leap of faith__: Instead of unrolling the recursion step by step (messy), assume the recursive call works as intended, and focus on how your current step relates to it. Instead of considering recursion a function calling itself over and over, consider solving one step and delegating the rest to a smaller version of myself.	
- Visualize the __call stack__: Every recursive call pauses the current function and pushes a new frame onto the stack. When the base case is hit, results bubble back up.

### Recursion Vs. Iteration

Recursive algorithms can be very space inefficient (each recursive call adds a new layer to the stack). It's often better to implement a recursive algorithm iteratively. All recursive algorithms can be implemented iteratively, although code complexity increases. Discuss tradeoffs.

### Dynamic programming & Memoization

**Dynamic programming problems**: Problems stated in terms of changing input data. Most general form: "Given a structure composed of objects, find efficient algorithms and data structures to answer certain queries about the structure, while also efficiently supporting update operations (such as insertion, deletion or modification of objects in the structure)".

Complexity measures used: space, initialization time, insertion time, deletion time, query time, etc.

**Approaches** to dynamic programming problems:

- Take a recursive algorithm and find the overlapping subproblems (i.e., the repeated calls). Then, cache those results for future recursive calls (memoization).
- Study the pattern of the recursive calls and implement something iterative. You still cache previous work.

**Example**: Compute the nth Fibonacci number. Different approaches:

- **Recursive** (top-down approach): Implement a normal recursive solution. No caching included.

```
int fibonacci(int i)
{
  if(n < 2) return n;
  return fibonacci(i - 1) + fibonacci(i - 2);
}
```

  - Drawing the number of recursive calls as a tree helps figure out the runtime of a recursive algorithm
  - Runtime: O(2<sup>n</sup>) (number of recursive calls)
  - Actually, runtime is closer to O(1.6<sup>n</sup>) since the right subtree of any node is always smaller than the left subtree. Either way, it's still exponential.

- **Top-down dynamic programming (or Memoization)**: In the recursive approach, we can see identical nodes in the recursion tree. We can solve this inefficiency using memoization (cache results to use them later), making it run in O(n) time.

```
int fibonacci(int n)
{
  std::vector<int> memo(n + 1, 0);
  return fibonacci(n, memo);
}

int fibonacci(int i, std::vector<int>& memo)
{
  if(n < 2) return n;
  
  if (!memo[i])
    memo[i] = fibonacci(i - 1, memo) + fibonacci(i - 2, memo);
	
  return memo[i];
}
```

  - The new tree has now depth ~n, and each of these node has one other child, resulting in ~2n children.
  - Runtime: O(n)

- **Bottom-up dynamic programming**: Doing the recursive memoized approach, but in reverse.

```
int fibonacci(int n)
{
  if(n < 2) return n;
  
  std::vector<int> memo(n, 0);
  memo[1] = 1;
  
  for(int i = 2; i < n; i++)
    memo[i] = memo[i-1] + memo[i-2];
  
  return memo[n-1] + memo[n-2];
}
```

Additional reading: Proof by induction


## System design and Scalability

Design an escalable system. Ask questions. Engage the interviewer. Discuss tradeoffs. There're good and bad solutions. There's no perfect solution, there're always tradeoffs. Two different designs for a system can be excellent, given different assumptions.

Goal: Understand use cases, scope a problem, make reasonable assumptions, create a solid design based on those assumptions, and be open about the weaknesses of your design. Don't expect something perfect.

### Handling the questions

The questions are mostly about the process rather than the ultimate design.

- **Communicate**: Show your ability to communicate. Engage the interviewer. Ask questions. Be open about issues of your system.
- **Go broad first**: Don't focus too much on one part or dive straight into the algorithm part.
- **Use the whiteboard**: It helps the interviewer follow your proposed design.
- **Acknowledge interviewer concerns**: Validate his concerns, acknowledge the issues, and make changes accordingly.
- **Be careful about assumptions**: Incorrect assumptions can dramatically change the problem.
- **State your assumptions explicitly**: This lets the interviewer correct you if you're mistaken, and shows that you know what assumptions you're making.
- **Estimate when necessary**: Sometimes you don't have the data you need.
- **Drive**: Stay in the driver's seat. Drive through the questions. Ask and talk to the interviewer. Be open about tradeoffs. Go deeper. Make improvements.

## Design

Designing a system begins by doing a lot of questions.

- **Scope the problem**: Ensure that you're building what the interviewer wants. Some questions must be answered before going further. List the major features or use cases.
- **Make reasonable assumptions**: When necessary. Talk about your assumptions.
- **Draw the major components**: Draw a diagram on the whiteboard. Walk through your system from end-to-end to provide a flow. It may help here to ignore major scalability challenges and just pretend that the simple, obvious approaches will be ok. You'll handle the big issues in the next step.
- **Identify the key issues**: Once you have a basic design, focus on the key issues. What will be the bottlenecks or major challenges in the system? If the interviewer provides some guidance, use it.
- **Redesign for the key issues**: Adjust your design for the key issues. It might be a minor tweaking or a major redesign. Update your diagrams on the whiteboard. Be open about any limitations in your design.

### Algorithms that scale

Sometimes you don't have to design an entire system, but a single feature or algorithm in an escalable way. Or maybe one algorithm part is the focus of a broader design question. Try this approach:

1. **Ask questions**: Make sure you really understand the question. Some details might be left out (intentionally or not).
2. **Make believe**: Pretend that the data can all fit on one machine and there's no memory limitations. How would you solve the problem? This is the general outline for your solution.
3. **Get real**: Go back to the original problem. How much data can fit on one machine? What problems will occur when you split up the data?
4. **Solve problems**: Think about how to solve the issues from step 2. Remove or mitigate each issue. Usually, you can continue using the outlined solution (with modifications), but occasionally you'll need to fundamentally alter it.

An iterative approach is typically useful (after solving problems from step 3, new problems may emerge, and you must tackle them as well).

Your goal is not to re-architect existing complex systems (expensive), but rather to demonstrate that you can analyze and solve problems. Poking holes in your solution is a great way to demonstrate this.

### Key concepts

- **Scaling types**: A system can be scaled one of two ways:
  - **Vertical**: Increase resources of a specific node (like adding additional memory to a server). Easier, but limited.
  - **Horizontal**: Increase number of nodes (like adding additional servers).

- **Load balancer**: Distributes the load evenly so that one server doesn't crash and take down the whole system. This requires a network of cloned servers that all have essentially the same code and access to the same data. Typically, some frontend parts of a scalable website are thrown behind a load balancer.

- **Database denormalization and NoSQL**: In a relational database (like SQL), information is often split into separate tables to avoid redundancy (normalization). A join operation "joins" two different tables together into a single result based on a related column (example: to see which customer placed which order, you "join" them using `customer_id`). This join can get very slow as the system grows bigger, so we generally want to avoid them. Two options:
  - **Denormalization**: Adding redundant information into a database to speed up reads. Example: Consider a database describing projects and tasks. We might need to get the project name and the task information. Rather than doing a join across these tables, we can store the project name within the task table (in addition to the project table).
  - **NoSQL** database: It doesn't support joins and might structure data in a different way. It's designed to scale better.

- **Database partitioning (Sharding)**: Split the data across multiple machines while ensuring there's a way to figure out which data is on which machine. There're different ways of partitioning (many architectures end up using multiple partitioning schemes):
  - **Vertical**: Partition by feature. In a social network, we might have one partition for tables relating profiles, another for messages, and so on. Drawback: If one table gets very large you might need to repartition that database (possibly using a different partitioning scheme).
  - **Key-based (or hash-based)**: Some part of the data (like an ID) is used to partition it. This can be done by allocating N servers and putting the data on `mod(key, n)`. Drawback: adding new servers requires allocating all the data (expensive).
  - **Directory-based**: Maintain a lookup table for where the data can be found. This makes it easy to add additional servers. Drawbacks: the lookup table is a single point of failure, and constantly accessing this table impacts performance.
  
- **Caching**: In-memory cache is a key-value pairing used for delivering rapid results. An application requesting a piece of information first tries the cache. It the cache doesn't contain the key, it looks up the data in the data store. When you cache, you might cache a query and its results directly; or, alternatively, the specific object (like a rendered version of part of the website, or a list of most recent blog posts).

- **Asynchronous processing & Queues**: Slow operations should ideally be done asynchronously, so users don't get stuck waiting for a process to complete. Some options:
  - **Pre-process**: Do it in advance. Example: a queue of jobs can update part of the website. In a forum, one job might re-render a page that lists the most popular posts and the number of comments, even if it's slightly out of date.
  - **Wait**: Tell the user to wait and notify when the process is done.

- **Networking metrics**: Important metrics around networking include:
  - **Bandwidth**: Maximum amount of data that can be transferred per unit of time (like bits/s or GB/s).
  - **Throughput**: Actual amount of data that is transferred per unit of time.
  - **Latency**: How long it takes data to go from one end to the other. Delay between the sender sending information and the receiver receiving it. Complicated to improve. Important for online games.
  - Example: Consider a conveyor belt for transferring items across a factory.
    - Fatter conveyor → Same latency. Higher throughput and bandwidth.
	- Shorter conveyor → Lower latency. Same throughput and bandwidth.
	- Faster conveyor → Lower latency, throughput and bandwidth.

- **MapReduce**: Typically used to process large amounts of data by parallelizing it. This makes processing more scalable. Two steps:
  1. `Map`: Takes in some data and emits a `<key, value>` pair
  2. `Reduce`: Takes a key and a set of associates values and "reduces" them in some way, emitting a new key and value. The result of this might be fed back into the `Reduce` program for more reducing.
  
### Considerations

Issues when designing a system:

- **Failures**: Any part of a system can fail. Plan for many or all failures.
- **Availability**: Function of the percentage of time the system is operational.
- **Reliability**: Function of the probability that the system is operational per unit of time.
- **Read-heavy vs. Write-heady**: Whether the application does a lot of reads or writes impacts the design. If it's write-heavy, consider queueing up the writes. If it's read-heavy, consider caching. Other designs decisions can change as well.
- **Security**: Consider the threats and issues the system might face and design around those.
- There're more potential issues. Be open about the tradeoffs.

### Example problem

**Problem**: Given a list of millions of documents, how would you find all documents that contain a list of words? The words can appear in any order, but must be complete words (`book` doesn't match `bookkeeper`).

1. **Ask questions**: `findWords` is a one time operation or is it called repeatedly? We will assume it's used many times for the same set of documents, and therefore we can accept the burden of pre-processing.

2. **Make believe**: Pretend we just have a few dozen documents. How would we implement `findWords` in this case? We could pre-process each document and create a hash-table index that maps from a word to a list of documents containing that word. Searching for a set of words requires just doing an intersection on the values for those words.

3. **Get real**: Go back to the original problem. What problems arise with millions of documents? We may need to divide up the documents across many machines. And may not be able to fit the full hash table on one machine. This introduce key concerns such as:
  1. How to divide up our hash table? By keyword (one machine has the full document list for a given word) or by document (one machine has the keyword mapping for a subset of the documents).
  2. How to process a document on one machine and push the results off to other machines? (not necessary if we divide the hash table by document).
  3. How to know which machine holds a piece of data? What does this lookup table looks like, and where is it stored?

4. **Solve problems**: Find solutions to each of the previous issues. Proposed solution:
  1. Divide up the words alphabetically by keyword, such that each machine controls a range of words.
  2. Iterate through the keywords alphabetically, storing as much data as possible on one machine. When it's full, move to the next machine.
    - Advantage: the lookup table is small and simple (it only specifies a range of values), and each machine can store a copy of the lookup table.
    - Disadvantage: Adding new documents or words require performing an expensive shift of keywords.
  3. To find all the documents that match a list of strings, we sort the list and send each machine a lookup request for the strings that the machine owns. Each machine looks up the document lists containing the requested strings and performs an intersection on them. Then, the initial machine does an intersections on the results from all machines.


## Sorting and Searching

Many sorting and searching problems are tweaks of well-known algorithms.

### Sorting

Common sorting algorithms:

- **Bubble sort**: O(n<sup>2</sup>) runtime (average & worst case). O(1) memory.

Swap the first two elements of the array if the first is greater than the second. Then, go to the next pair, and so on, continuously making sweeps of the array until it's sorted. Smaller items slowly "bubble" up to the beginning of the list. Every traversal moves the biggest element to the right.

- **Selection sort**: O(<sup>2</sup>) runtime (average & worst case). O(1) memory.

Find the smallest element using a linear scan and move it to the front (swapping it with the front element). Repeat with the second smallest element. Continue until all elements are in place. Simple, but inefficient.

- **Merge sort**: O(n log n) runtime (average & worst case). O(n) memory.

Divide the array in half, sort each halve, and merge them back together. Merge sort is applied to each halve. Eventually, you're merging just two single element arrays. The `merge` part does all the heavy lifting: it copies all elements from the target array segment into `helper` array, keeping track of where the start of the left and right halves should be (`helperLeft` and `helperRight`). We then itereate through `helper`, copying the smaller element from each half into the array.

At the end, we copy any remaining elements (from the left half of `helper`) into the target array. The right half doesn't need to be copied becasue it's already there. Example: Consider halves `1, 4, 5` and `2, 8, 9`. Prior to merging the two halves, both the helper array and target array segment will end with `8, 9`, so there's no need to copy them over.

- **Quick sort**: O(n log n) (average case) or O(n<sup>2</sup>) (worst case) runtime. O(log n) memory.

Pick a random element and partition the array, such that all numbers that are less than the partitioning element come before all elements that are greater than it. Partitioning is done efficiently through a series of swaps. If we repeatedly partition the array (and its sub-arrays) around an element, the array will eventually become sorted. However, the partitioned element is not guaranteed to be the median (or near), so the algorithm could be very slow in the worst case.

- **Radix sort**: O(kn) runtime (n: number of elements. k: number of passes of the sorting algorithm).

Sorting algorithm for integers (and some other data types) that takes advantage of the fact that integers have a finite number of bits. Iterate through each digit of the number, grouping numbers by each digit. Example: Given an array of integers, we sort by the first digit, then each group is sorted by the next digit, and so on, until finally the whole array is sorted.

Unlike comparison algorithms, which cannot perform better than O(n log n) in the average case, Radix sort has O(kn) runtime. 

### Searching

The most common searching algorithm is Binary search, but there're more options. You might, for example, search for a node by leveraging a binary tree, or by using a hash table.

In **binary search**, we look for an element x in a sorted array by first comparing x to the midpoint of the array. If x is less than the midpoint, search the left half. If x is greater, search the right half. Repeat this until you find x or the subarray has size 0. This can be done iteratively or recursively.


## Testing

### Purpose

**The interviewer looks for:**

- **Test cases**: Coming up with a reasonable list of test cases.
- **Understand the big picture**: Understand what is the software really about and prioritize test cases properly. Example: in an e-commerce, it's good that product images appear correctly, but it's more important that payments work reliably.
- **Know how the pieces fit together**: Understand how software works, and how it might fit in a greater ecosystem. Example: For Google Spreadsheets we need to test its integration with Gmail, with plug-ins, and with other components.
- **Organization**: Approach the problem in a structured manner. Break the problem into categories to do a more thorough job creating test cases. Example: Testing a camera can be broken down into Taking photos, Image management, Setting, etc.
- **Practicality**: Create reasonable testing plans. Testing plans need to be feasible and realistic for a company to implement.

### Testing problems

In testing problems, don't expect nice input/users, but expect abuse and plan for it.

Typical **types of testing problems**:

- **Test a real world object** (like testing a pen or a paperclip)
- **Test a piece of software**
- **Test a function**
- **Troubleshoot an existing issue**

### Test a real world object**:

- **Who will use it? And why?** Answering this will shape how you handle the remaining questions.
  - Example: teachers, to hold papers together; or artists, to bend into the shape of an animal.
- **What are the use cases?**
  - Example: a product needs to be able to send and receive content, or write and erase.
- **What are the bound of use?**
  - Example: holding up to 30 sheets of paper in a single usage without permanent damage (bending), and 30-50 sheets with minimal permanent bending; or working during very warm temperatures (90-110º), or extreme cold.
- **What are the stress/failure conditions?** Discuss when it's acceptable, or even necessary, for the product to fail, and what failure should mean.
  - Example: a laundry machine should be able to handle at least 30 shirts/pants. Loading 30-45 pieces may cause minor failure (inadequate cleaning). For more than 45 pieces, extreme failure (machine never turning on the water) might be acceptable.
- **How would you perform the testing?**
  - Example: to test whether a chair can withstand normal usage for five years, you'd need to define what "normal" usage is (how many sits per year? what about the armrest?). Additionally, we may want a machine to automate some of the usage.

### Test a piece of software

Similar to testing a real world object, but placing greater emphasis on the details of performing testing.

**Core aspects**:

- **Manual vs. Automated** testing: We want to automate everything, but this is rarely feasible. Some things are much better with manual testing because some features are too qualitative for a computer to effectively examine (like identifying pornography). Additionally, human observation may reveal new issues that haven't been specifically examined.

- **Black box vs. White box** testing: Degree of access we have into the software. We may receive the software as-is (black box) to test it, or have programmatic access to test individual functions (white box). Automating black box testing is much harder.

**Approach**:

1. **Are we doing Black or White box testing (or both)?** 
2. **Who will use it? And why?** Features are designed with the target user/s in mind. For a parental control on a web browser, the target users are parents (implement blocking), children (get blocked), and guests (neither block, nor get blocked).
3. **What are the use cases?** This is not your decision, so discuss this with the interviewer. The parental control use cases for parents include installing the software, updating controls, removing controls, and their own personal internet usage. For children include accessing legal and "illegal" content.
4. **What are the bounds of use?** Define what is a blocked website. Specify what is blocked (just the "illegal" page or the entire website). Specify if the application learns what is bad content or if it's based on a white or black list. If it learns, specify the acceptable degree of false positives and false negatives.
5. **What are the stress conditions/failure conditions?** What should failure look like? A failure shouldn't crash the computer. Instead, maybe the software should just permit a blocked site, or ban an allowable site.
6. **What are the test cases? How would you perform the testing?** It depends on whether it's manual or automatic testing, and black box or white box testing. Step 3 and 4 should have roughly defined the use cases. Now we further define them and discuss how to perform the testing. What exact situations are you testing? Which steps can be automated? Which require human intervention. 

Going through that list just by including every scenario you can think of is disorganized and makes you miss major categories. Approach it in a structured manner. Break down your testing into the main components, and go from there. This will give you a more complete list of test cases, and shows that you're a structured, methodical person.

### Test a function

It's the easiest type of testing. Testing is usually limited to validating input and output. Discuss any assumptions, particularly with respect to how to handle specific situations. Example: Test `sort(int* array[])` (sorts an array of integers).

- **Define test cases**: This requires knowledge of the function. If constraints are unclear, ask for clarification. Types of test cases:
  - **Normal case**: Does it generate the correct output for typical inputs? Think about potential issues here. Example: Sorting often requires partitioning, so the algorithm could fail on arrays with an odd number of elements, since they cannot be evenly partitioned.
  - **The extremes**: Like passing an empty array, a very small (one element) one, or a very large one.
  - **Nulls and "illegal" input**: How the code should behave when given illegal input? Like passing a negative input to `getNthFiboNumber(int n)`.
  - **Strange input**: What if you pass an already sorted array? Or one sorted in reverse order?
- **Define the expected result**: The expected result is often the right output. In some cases, you might want to validate additional aspects. Example: if `sort()` returns a new sorted copy of the array, maybe you should validate that the original array was not touched.
- **Write test code**: Once you have the test cases and results defined, write code to implement the test cases. Example:

```
void testAddThreeSorted()
{
  MyList list;
  list.addThreeSorted(3, 1, 2);   // Adds 3 items in sorted order
  
  assert(list.getElement(0) == 1);
  assert(list.getElement(1) == 2);
  assert(list.getElement(2) == 3);
}
```

### Troubleshoot an existing issue

Explain how to debug or troubleshoot an existing issue. Approach this in a structured manner. 

Example problem: The Google Chrome team receives a bug report: "Chrome crashes on launch". What would you do? Don't give unrealistic answers like "reinstall the software" (it might solve this user's problem, but wouldn't help the other users experiencing this problem). Your goal is to understand what's really happening, so that the developers can fix it.

- **Understand the scenario**: Ask questions. 
  - How long has the user been experiencing this issue?
  - What browser version is it? What OS?
  - Does the issue happen consistently, or how often does it happen? When does it happen?
  - Is there an error report that launches?
- **Break down the problem**: Break the problem into testable units. Situation flow example:
  1. Go to Windows Start menu > Click on Chrome icon
  2. Browser instance starts
  3. Browser loads settings
  4. Browser issues HTTP request for homepage
  5. Browser gets HTTP response
  6. Browser parses webpage
  7. Browser displays content  
  - At some point in this process, something fails and causes the browser crash. Iterate through the elements of this scenario to diagnose the problem.
- **Create specific, manageable tests**: Each of the above components should have realistic instructions (things that you can ask the user to do, or that you can do yourself to replicate steps on your machine).


## C and C++

Good interviewers will let you code in a language you know. Most interviewers won't care if you don't remember all the APIs. However, it's recommended to study up on basic C++ syntax.

### Classes and Inheritance

The code below implements a basic class with inheritance. All data members and methods are private by default. This can be modified by introducing the keyword `public`.

```
#include <iostream>
using namespace std;

#define NAME_SIZE 50   // defines a macro

class Person
{
  int id;
  char name[NAME_SIZE];
  
public:
  void aboutMe() { cout << "I'm a person."; }
};

class Student : public Person
{
public:
  void aboutMe() { cout << "I'm a student."; }
};

int main()
{
  Student* p = new Student();
  p->aboutMe();   // prints "I'm a student."
  delete p;   // delete allocated memory
  return 0;
}
```

### Constructors and Destructors

The **constructor** of a class is automatically called upon an object's creation. We can define our own constructors. Otherwise, the compiler automatically generates one (Default Constructor). Two options:

- **Simple way**:

```
Person(int a) { id = a; }
```

- **Member initializer list**: This initializes `id` before the actual object is created and before the remainder of the constructor code is called. This is necessary when the fields are constant or class types.

```
Person(int a) : id(a) { ... }
```

The **destructor** cleans up upon object deletion and is automatically called when an object is destroyed. It cannot take an argument as we don't explicitly call a destructor.

```
~Person() { delete obj; }
```

### Virtual functions

We can assign a `Student*` object (child) to a `Person*` object (parent). Here, `p->aboutMe()` prints `I'm a person` because the function is resolved at compile-time (static binding).

```
Person* p = new Student();
p->aboutMe();   // prints "I'm a person."
```

We can ensure that `Student::aboutMe` is called by defining `Person::aboutMe` to be a **virtual function**.

```
class Person
{
  ...
  virtual void aboutMe() { cout << "I'm a person."; }
};

class Student : public Person
{
public:
  void aboutMe() { cout << "I'm a student."; }
};
```

Virtual functions are also useful when we can't, or don't want to, implement a method for the parent class. Defining`Person::addCourse` to be a **pure virtual function** makes `Person` an abstract class and we cannot instantiate it.

```
class Person
{
  ...
  virtual bool addCourse(string s) = 0;
};

class Student : public Person
{
  ...
  bool addCourse(string s)
  {
    cout << "Added course: " << s << endl;
	return true;
  }
};

int main()
{
  Person* p = new Student();
  p->aboutMe();   // prints "I'm a student."
  p->addCourse("History");
  delete p;
}
```

### Virtual destructor

If we include normal destructors in `Person` and `Student`:

```
class Person
{
  ...
  ~Person() { cout << "Deleting a person." << endl; }
};

class Student : public Person
{
  ...
  ~Student() { cout << "Deleting a student." << endl; }
};

int main()
{
  Person* p = new Student();
  delete p;   // prints "Deleting a person"
}
```

Here, only the `Person` destructor is called. This is problematic because the memory of `Student` may not be cleaned up. This is fixed by defining the destructor of `Person` to be virtual.

```
class Person
{
  ...
  virtual ~Person() { cout << "Deleting a person." << endl; }
};
```

This will output the following:

```
Deleting a student.
Deleting a person.
```

### Default values

Functions can specify default values. All default parameters must be on the right side of the function declaration.

```
int func(int a, int b = 3) { return a + b; }

x = func(4);   // == 4 + 3
y = func(4, 5);   // == 4 + 5
```

### Operator overloading

Operator overloading enables us to apply operators (like `+`) to objects that would otherwise not support these operations.

```
BookShelf BookShelf::operator+(BookShelf &other) {...}
```

### Pointers and References

A **pointer** holds the address of a variable and can be used to perform any operation that could be directly done on the variable, such as accessing and modifying it.

If two pointers equal each other, changing one's value also changes the other's value, since both point to the same address.

```
int *a = new int;
*a = 7;
int *b = a;
*a = 8;
cout << *b;   // prints 8
```

The size of a pointer depends on the architecture: 32 bits on a 32-bit machine, and 64 bits on a 64-bit machine. This knowledge is valuable when calculating how much space a data structure takes up.

A **reference** is another name (alias) for a pre-existing object and it doesn't have memory of its own.

```
int a = 5;
int &b = a;   // b is a reference to a
b = 7;
cout << a;   // print 7
```

A reference cannot be created without specifying where in memory it refers to. However, we can create a free-standing reference(`const int &b = 12` → allocates memory for `12` and makes `b` a reference to this memory).

Unlike pointers, references cannot be `null` and cannot be reassigned to another piece of memory.

**Pointer arithmetic**: Performing addition (`++`) on a pointer will skip ahead as many bytes as the size of the pointed data structure.

```
int *p = new int[2];
p[0] = 0;
p[1] = 1;
p++;   // skips ahead by sizeof(int) bytes
cout << *p;   // outputs 1
```

### Templates

Templates are a way of reusing code to apply the same class to different data types. The code below implements a data structure:

```
template <class T>
class ShiftedList
{
  T* array;
  int offset, size;
public:
  ShiftedList(int sz) : offset(0), size(sz) { array = new T[size]; }
  ~ShiftedList() { delete[] array; }
  void shiftBy(int n) { offset = (offset + n) % size; }
  T getAt(int i) { return array[convertIndex(i)]; }
  void setAt(T item, int i) { array[convertIndex(i)] = item; }
  
private:
  int convertIndex(int i)
  {
    int index = (i  offset) % size;
	while (index < 0) index += size;
	return index;
  }
};
```


## Java

Language and syntax questions are more unusual at bigger companies, which prefer testing aptitude rather than knowledge (and which have time and resources for training candidates in a particular language). In other companies, these questions can be quite common.

### Approach

The best options to master these questions is to learn Java inside and out. But, if you get stumped, try this approach (this helps to derive an answer):

1. Create an example of the scenario, and ask yourself how things should play out.
2. Ask yourself how other languages would handle this scenario.
3. Consider how you would design this situation if you were the language designer. What would the implications of each choice be?

### Overloading vs. Overriding

**Overloading**: Describes when two methods have the same name but differ in the type or number of arguments.

```
public double computeArea(Circle c) { ... }
public double computeArea(Square s) { ... }
```

**Overriding**: Describes when a method shares the same name and function signature as another method in its super class.

```
public abstract class Shape
{
  public void printMe() { System.out.println("I'm a shape"); }
  public abstract double computeArea();
}

public class Circle extends Shape
{
  private double rad = 5;
  public void printMe() { System.out.println("I'm a circle"); }
  public double computeArea() { return rad * rad * 3.15; }
}

public class Ambiguous extends Shape
{
  private double area = 10;
  public double computeArea() { return area; }
}

public class IntroductionOverriding
{
  public static void main(String[] args)
  {
    Shape[] shapes = new Shape[2];
	Circle circle = new Circle();
	Ambiguous ambiguous = new Ambiguous();
	
	shapes[0] = circle;
	shapes[1] = ambiguous;
	
	for (Shape s : shapes)
	{
	  s.printMe();
	  System.out.println(s.computeArea());
	}
  }
}
```

Output:

```
I'm a circle
78.75
I'm a shape
10.0
```

`Circle` overrode `printMe()`, whereas `Ambiguous` just left this method as-is.

### Collection Framework

Java's collection framework is highly useful. Most useful items are:

- **`ArrayList`** (`std::vector`): Dynamically resizing array, which grows as you insert elements.

```
ArrayList<String> myArr = new ArrayList<String>();
myArr.add("one");
myArr.add("two");
System.out.println(myArr.get(0));   /* prints <one> */
```

- **`Vector`**: Similar to `ArrayList`, except that it's synchronized. It's syntax is almost identical.

```
Vector<String> myVec = new Vector<String>();
myVec.add("one");
myVec.add("two");
System.out.println(myVec.get(0));
```

- **`LinkedList`** (`std::list`): Java's built-in linked list. Rarely used. It demonstrates some of the syntax for an iterator.

```
LinkedList<String> myLinkedList = new LinkedList<String>();
myLinkedList.add("two");
myLinkedList.addFirst("one");
Iterator<String> iter = myLinkedList.iterator();
System.out.println(myLinkedList.get(0));
while (iter.hasNext())
  System.out.println(iter.next());
```

- **`HashMap`**: Java's built in hash-map. Widely used.

```
HashMap<String, String> map = new HashMap<String, String>();
map.put("one", "uno");
map.put("two", "dos");
System.out.println(map.get("one"));
```


## Databases

There're different flavors of SQL. You might have worked with a slightly different one, so don't be surprised by minor syntax variations.

### SQL syntax and variations

The following implicit and explicit joins are equivalent. Any of them is valid.

- **Explicit join** (our choice):

```
SELECT CourseName, TeacherName
FROM Courses INNER JOIN Teachers
ON Courses. TeacherID = Teachers.TeacherID
```

- **Implicit join**:

```
SELECT CourseName, TeacherName
FROM Courses, Teachers
WHERE Courses.TeacherID = Teachers.TeacherID
```

### Denormalized vs. Normalized databases

**Normalized** databases are designed to minimize redundancy. One type of information is only stored once in the database, but many common queries will require expensive joins. Example: `Courses` table might contain a column called `TeacherID`, which is a foreign key to `Teacher` table.
  
**Denormalized** databases are designed to optimize read time by storing redundant data. Useful for creating highly scalable systems. Example: If we repeat this query often, we can store the teacher's name in `Courses` table.

### SQL statements

Consider this structure (`*` indicates a primary key):

```
Courses: CourseID*, CourseName, TeacherID
Teachers: TeacherID*, TeacherName
Students: StudentID*, StudentName
StudentCourses: CourseID*, StudentID*
```

**Query 1: Student enrollment**: Get a list of all students and how many courses each student is enrolled in.

- Incorrect solution:

```
/* Incorrect code */
SELECT Students.StudentName, count(*)
FROM Students INNER JOIN StudentCourses
ON Students.StudentID = StudentCourses.StudentID
GROUP BY Students.StudentID
```

  - Problems:
    - We exclude students who are not enrolled in any courses (`StudentCourses` only includes enrolled students). We need to change this to a `LEFT JOIN`.
    - Even changing it to `LEFT JOIN`, the query is still not quite right. Doing `count(*)` returns how many items there're in a given group of `StudentIDs`. Students enrolled in zero courses would still have one item in their group. We need to change this to count the number of `CourseIDs` in each group: `count(StudentCourses.CourseID)`
    - We've grouped by `Students.StudentID`, but there're still multiple `StudentNames` in each group. The database doesn't know which `StudentName` to return, even though they may all have the same value. We need to apply an *aggregate* function like `first(Students.StudentName)`.

- Solution 1: Wrap with another query (fixes previous problems)

```
SELECT StudentName, Students.StudentID, Cnt
FROM (
  SELECT Students.StudentID, count(StudentCourses.CourseID) as [Cnt]
  FROM Students LEFT JOIN StudentCourses
  ON Students.StudentID = StudentCourses.StudentID
  GROUP BY Students.StudentID
) TINNER JOIN Students on T.studentID = Students.StudentID 
```

  - Why we don't just select the student name on line 2 to avoid having to wrap lines 2 through 5 with another query? We can't do that. We can only select values that are in an aggregate function or in the `GROUP BY` clause.
  
```
/* Incorrect code */
SELECT StudentName, Students.StudentID, count(StudentCourses.CourseID) as [Cnt]
FROM Students LEFT JOIN StudentCourses
ON Students.StudentID = StudentCourses.StudentID
GROUP BY Students.StudentID
```

- Solution 2: Add `StudentName` to `GROUP BY` clause.

```
SELECT StudentName, Students.StudentID, count(StudentCourses.CourseID) as [Cnt]
FROM Students LEFT JOIN StudentCourses
ON Students.StudentID = StudentCourses.StudentID
GROUP BY Students.StudentID, Students.StudentName
```

- Solution 3: Wrap with aggregate function.

```
SELECT max(StudentName) as [StudentName], Students.StudentID, count(StudentCourses.CourseID) as [Count]
FROM Students LEFT JOIN StudentCourses
ON Students.StudentID = StudentCourses.StudentID
GROUP BY Students.StudentID
```

**Query 2: Teacher class size**: Get a list of all teachers and how many students they each teach. If the teacher teaches the same student in two courses, you should double count the student. Sort the list in descending order of the number of students a techer teaches.

```
SELECT TeacherName, isnull(StudentSize.Number, 0)
FROM Teachers LEFT JOIN
  (SELECT TeacherID, count(StudentCourses.CourseID) AS [Number]
  FROM Courses INNER JOIN StudentCourses
  ON Courses.CourseID = StudentCourses.CourseID
  GROUP BY Courses.TeacherID) StudentSize
ON Teachers.TeacherID = StudentSize.TeacherID
ORDER BY StudentSize.Number DESC
```

- We construct this query step by step. First, get a list of `TeacherIDs` and how many students are associated with each `TeacherID` (lines 3-6).
- The `INNER JOIN` won't select teachers who aren't teaching classes. That's handled in the below query when we join it with the list of all teachers.
- Note how we handled the `NULL` values in the `SELECT` statement to convert the `NULL` values to zeros.

### Small database design

The approach for designing your own database is similar to the approach for object-oriented design.

1. **Handle ambiguity**: Understand exactly what you need to design. Database questions often have some ambiguity (intentionally or unintentionally).

  - Example: Design a system to represent an apartment rental agency.
    - How many locations has this agency?
	- How general should this system be? For example, it's extremely rare for a person to rent 2 apartments in the same building, but shouldn't you be able to handle that? Maybe, maybe not. Some very rare conditions might be best handled through a work around (like duplicating the person's contact information in the database).
	
2. **Define core objects**: Each core object typically translates into a table.

  - Example: `Property`, `Building`, `Apartment`, `Tenant`, `Manager`.

3. **Analyze relationships**: What the tables should be? How do them relate to each other? Are they many-to-many or one-to-many?

  - If `Buildings` has one-to-many relationship with `Apartments` (one `Building` has many `Apartments`), then we might represent this as follows (note that `Apartments` links back to `Buildings` with a `BuildingID` column):

```
Apartments
  ApartmentID (int)
  ApartmentAddress (varchar(100))
  BuildingID (int)

Buildings
  BuildingID (int)
  BuildingName (varchar(100))
  BuildingAddress (varchar(500))
```

  - To allow for the possibility that one person rents more than one apartment, we might want to implement a many-to-many relationship as follows (`TenantApartments` stores a relationship between `Tenants` and `Apartments`):

```
TenantApartments
  TenantID (int)
  ApartmentID (int)
  
Apartments
  ApartmentID (int)
  ApartmentAddress (varchar(500))
  BuildingID (int)

Tenants
  TenantID (int)
  TenantName (varchar(100))
  TenantAddress (varchar(500))
```

4. **Investigate actions**: Walk through the common actions that will be taken and understand how to store and retrieve the relevant data. Each action requires new tables and columns.

  - We need to handle lease terms, moving out, rent payments, etc.

### Large database design

When designing a large, scalable database, joins (required in the above examples) are generally very slow. Thus, you must **denormalize** your data. Think carefully about how data will be used (probably, you will need to duplicate data in multiple tables).


## Threads and Locks

C++ treats a thread as a resource (like memory or a file handle). When a standalone application is run, a user thread is automatically created to execute the `main()` method. We use the `<thread>` header and the `std::thread` class to create new threads. If a `std::thread` object is destroyed (goes out of scope) before calling `.join()` (wait for it) or `.detach()` (let it run in the background), the program crashes (`std::terminate()` is called). It uses shared memory, managed by you (high risk of "race conditions").

You can pass almost anything "callable" (function pointer, lambda, or functor) directly to the `std::thread` constructor.

- **Passing a function**:

```
#include <iostream>
#include <thread>
#include <chrono> // For milliseconds
#include <atomic> // For thread-safe flags

std::atomic<bool> should_stop(false);

void task()
{
    std::cout << "Thread starting\n";

    int count = 0;
    while (count < 5)
	{
        if (should_stop)
		{
            std::cout << "Thread interrupted\n";
            break; 
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
        count++;
    }

    std::cout << "Thread terminating\n";
}

int main()
{
    std::thread t1(task);
    std::this_thread::sleep_for(std::chrono::milliseconds(1200));
    should_stop = true; 
    t1.join();
    return 0;
}
```

Why not use `bool should_stop`? Because it's unrealiable:

  - CPU caching: 


- **Passing a function (C++20)**: `std::jthread` (Joining Thread) automatically joins when it goes out of scope. It includes a built-in `stop_token` that replaces `should_stop`. It still allows using `.join()` and `.detach()`.

```
void task(std::stop_token stoken)
{
    std::cout << "Thread starting\n";

    int count = 0;
    while (count < 5)
	{
        if (stoken.stop_requested())
		{
            std::cout << "Thread interrupted\n";
            return; 
        }

        std::this_thread::sleep_for(std::chrono::milliseconds(500));
        count++;
    }
}

int main()
{
    std::jthread jt(task);
    std::this_thread::sleep_for(std::chrono::seconds(2));
    jt.request_stop();   // this is also called by jt's destructor
	jt.join();   // optional
    return 0;
}
```

- **Passing a functor**:

```

```










void task()
{
    std::cout << "Thread starting" << std::endl;
		
	try
	{
	  int count = 0;
	  while (count < 5)
	  {
	    std::this_thread::sleep_for(std::chrono::milliseconds(500));
		count++;
	  }
	}
	catch (InterruptedException exc) {
	  std::cout << "Thread interrupted" << std::endl;
	}
	
	std::cout << "Thread terminating" << std::endl;
}

int main()
{
    std::thread t1(task);
    t1.join();
    return 0;
}
```

- **Passing a functor**:

```
class MyTask
{
public:
    void operator()() { std::cout << "Thread running from a class" << std::endl; }
};

// Usage
MyTask taskObj;
std::thread t2(taskObj); 
t2.join();
```






Every thread in Java is created and controlled by a unique object of the java. lang. Thread class. When a standalone application is run, a user thread is automatically created to execute the main () method. This thread is called the main thread. In Java, we can implement threads in one of two ways:

- By implementing the java. lang. Runnable interface 
- By extending the java. lang. Thread class 

We will cover both of these below. 

**Implementing the Runnable Interface**:

The Runnable interface has the following very simple structure. 

```
public interface Runnable
{ 
  void run(); 
}
```

To create and use a thread using this interface, we do the following: 

1. Create a class which implements the Runnable interface. An object of this class is a Runnable object.
2. Create an object of type Thread by passing a Runnable object as argument to the Thread constructor.
The Thread object now has a Runnable object that implements the run () method.
3. The start() method is invoked on the Thread object created in the previous step.
For example: 

public class RunnableThreadExample implements Runnable
{ 
  public int count = 0; 
  
  public void run()
  { 
    System.out.println("RunnableThread starting.");
    try { 
      while (count< 5)
	  { 
        Thread. sleep(500); 
        count++; 
      } 
    } catch (InterruptedException exc) { 
      System.out.println("RunnableThread interrupted."); 
      } 
    system.out.println("RunnableThread terminating."); 
  } 
}

public static void main(String[] args)
{ 
  RunnableThreadExample instance = new RunnableThreadExample(); 
  Thread thread= new Thread(instance); 
  thread.start(); 
 
  while (instance.count != 5)   // waits until above thread counts to 5 (slowly)
  { 
    try { 
      Thread.sleep(250); 
    } catch (InterruptedException exc) { 
      exc.printStackTrace(); 
    } 
  } 
} 
In the above code, observe that all we really needed to do is have our class implement the run () method (line 4). Another method can then pass an instance of the class to new Th read (obj) (lines 19 - 20) and call start() on the thread (line 21 ). 

In the above code, observe that all we really needed to do is have our class implement the run () method (line 4). Another method can then pass an instance of the class to new Th read (obj) (lines 19 - 20) and call start() on the thread (line 21 ).




Symbols: ≤, ≥, ≠, ≈, √, ∑, →, ↔, ∨, ∧, ~, ¬, ∀, ∃, ⌊⌋, ⌈⌉, <sub>i</sub>, <sup>i</sup>, α, β, ∞, Ω, Θ, θ, ϕ, γ, ├─, │, └─, …

## Moderate

## Hard


## Notes

- A list of size n have indices in range [0, n-1].
- `n / 2` = Element in the middle ([0][1]**[2]**[3][4]) or right after the middle ([0][1]**[2]**[3]).
- `n - 1 - i` = Opposing index ([0]**[1]**[2]**[3]**[4]).
- Storing elements of a list in a stack gets the list reversed.
- Passing elements from one stack to another inverts the order of the elements.

## Technical patterns

These patterns can handle roughly ~90% of common technical interview questions. Most questions are variations or combinations of these patterns.

- **Nested loop traversal** (O(n<sup>2</sup>)): One loop inside another loop.
  - When:
  - Sub-patterns:
  - Examples:
    - Palindromic substrings (O(n<sup>2</sup>))
	- All subarrays
	- All substrings

- **Pairwise comparison / All-pairs iteration** (O(n<sup>2</sup>)): Nested loop traversal where the outer loop iterates through each element, and the inner loop iterates over the elements after the current one. Brute-force all combinations.
  - When: Check for duplicates, find pairs with some property, compare all possible combinations.
  - Examples:
    - Closest pair of points
	- 2-sum brute force
	- Check duplicates in array
  
- **Two pointers / Runner technique**: Use two indices moving through a list to avoid nested loops.
  - When: Sorted arrays, find pairs with a sum, reverse strings in-place, remove duplicates.
  - Sub-patterns: Opposite ends, same-direction pointers, fast/slow pointers.
  - Examples:
    - Sorted array two-sum → Find if two numbers sum to a target.
	- Container with most water → Maximize area between two lines.
    - Remove duplicates from sorted array → In-place removal using read/write pointers.
	- Container with most water.
	- 3-sum problem.
	- Linked list cycle detection (Floyd's algorithm).
	
- **Sliding window**: Maintain a contiguous range (window) over data and slide it to track sums, counts, or max/min.
  - When: Substring/array problems involving a length or sum constraint.
  - Sub-patterns: Fixed-size window, dynamic-size window, string window problems.
  - Examples:
    - Longest substring without repeating characters → Variable-length window.
    - Minimum window substring → Dynamic shrinking and expanding window.
    - Longest repeating character replacement → Fixed-size window with char counts.
	- Maximum sum subarray of size k.
  
- **Fast & slow pointers** (or **Tortoise and hare**): Two pointers moving at different speeds to detect cycles or middle elements.
  - When: Linked-lists, circular arrays.
  - Sub-patterns: Cycle detection, middle finding, length of cycle.
  - Examples:
    - Linked list cycle detection → Floyd’s Tortoise and Hare.
    - Happy number → Detect loop in digit-sum transformation.
    - Find middle of linked list → Move one pointer twice as fast.
	- Reorder linked-list.
  
- **Hashing/Hash-map lookup**: Store visited elements or counts for O(1) lookups.
  - When: Detect duplicates, frequency counts, prefix sums.
  - Sub-patterns: Frequency maps, hash sets, rolling hash.
  - Examples:
    - Two sum
	- Group anagrams
	- Longest consecutive sequence
	
- **Binary search**: 
  - When:
  - Sub-patterns: Iterative, recursive, binary search on answer space.
  - Examples:
    - Search in Rotated Sorted Array
    - Find Minimum in Rotated Sorted Array
    - Median of Two Sorted Arrays  
	
- **BST (Binary Search Tree)**:
  - When:
  - Sub-patterns: In-order traversal, insertion/deletion, lowest common ancestor.
  - Examples:
    - Validate BST
    - Lowest Common Ancestor of BST
    - Convert Sorted Array to BST
  
- **Sorting + Binary search**: Sort data to apply binary search or fimplify constraints.
  - When: Search problems, interval merging, deduplication.
  
- **Graph traversal**: Explore data structures (graphs, grids, trees) systematically.
  - When: Connectivity, shortest path, tree processing.
  - Sub-patterns: BFS, DFS, Union-Find, Dijkstra's, Bellman-Ford.
  - Examples:
    - Number of connected components (islands) → Flood fill BFS/DFS.
    - Clone graph → BFS/DFS with visited map.
    - Word ladder → BFS shortest path on word graph.
	- Minimum spanning tree (Kruskal / Prim)
	
- **BFS (Breadth-First Search)**:
  - When:
  - Sub-patterns: Level-order traversal, shortest path in unweighted graphs.
  - Examples:
    - Binary tree level order traversal
	- Minimum depth of binary tree
	- Word ladder
	
- **DFS (Depth-First Search)**:
  - When:
  - Sub-patterns: Preorder/inorder/postorder, recursive vs. iterative.
  - Examples:
    - Binary tree path sum
	- Number of islands
	- Word search
  
- **Backtracking**: Try all possible choices, backtrack when a choice fails.
  - When: Combinatorics, permutations, constraint satisfaction.
  - Sub-patterns: DFS + decision-making, constraint-based recursion.
  - Examples:
    - N-Queens
	- Word search
	- Permutations/Combinations
  
- **Dynamic programming (DP)**: Break problems into overlapping subproblems and reuse results.
  - When: Optimization problems, sequences, combinatorics.
  - Sub-patterns: 1D DP (Fibonacci, Coin change), 2D DP (Knapsack, Grid paths), Interval DP (Palindromic substrings).
  - Examples:
    - Climbing stairs → Fibonacci DP.
    - Coin change → Min coins to reach amount.
    - Longest common subsequence → Classic DP table.
	- Longest common subsequence
	- House robber
	- Edit distance
  
- **Greedy algorithms**: Always take the locally optimal choice.
  - When: Interval scheduling, coin change (specific denominations), Huffman coding.
  - Sub-patterns: Interval scheduling, coin change (when greedy works), Huffma coding.
  - Examples:
    - Activity selection
	- Jump game
	- Huffman encoding
  
- **Union-Find / Disjoint set**: Keep track of connected components efficiently. Kruskal's algorithm.
  - When: Graph connectivity, Kruskal's algorithm.
  - Examples:
    - Redundant connection
	- Number of connected components
	- Accounts merge
  
- **Heap / Priority queue**: Always fetch min/max element efficiently.
  - When: Kth largest element, merging sorted lists.
  - Sub-patterns: Min-heap, max-heap, k-way merge.
  - Examples:
    - Kth largest element
	- Merge k sorted lists
	- Top K frequent elements.
  
- **Matrix traversal patterns**: Row/column scanning (row-by-row, column-by-column), spiral order, diagonal, boundary first, DFS/BFS on grids.
  - When: Board games, image processing.
  - Sub-patterns:
  - Examples:
    - Spiral matrix
	- Rotate image
	- Word search
  
- **Pairwise comparison / Nested loops**: Compare each element with the rest. Brute-force all combinations.
  - When: Closest points, brute-force matching.
  - Sub-patterns:
  - Examples:
    - Closest pair of points
	- 2-sum brute force
	- Check duplicates in array
  
- **Bit manipulation**: Use bitwise ops for compact storage or fast computation.
  - When: Flags, subsets, parity checks.
  - Sub-patterns: Masking, XOR tricks, bit DP.
  - Examples:
    - Single number → XOR to find unique element.
    - Find missing number → XOR all indices and elements.
    - Two single numbers → Partition by set bit.
	- Subsets using bitmask
	- Reverse bits
  
- **Prefix sum / Cumulative sum**: Precompute running sums to answer range queries fast.
  - When: Range sum queries, subarray sums.
  - Sub-patterns: 1D prefix sum, 2D prefix sum, difference array.
  - Example:
    - Subarray sum equals K
	- Range sum query (immutable)
	- 2D matrix sum region query
  
- **Merge intervals**: 
  - When:
  - Sub-patterns: Sorting by start time, merging, interval insertion.
  - Examples:
    - Merge intervals.
	- Insert interval.
	- Employee free time.
	
- **Cyclic sort**: 
  - When:
  - Sub-patterns: In-place index placement, missing number detection.
  - Examples:
    - Find all missing numbers.
	- First missing positive.
	- Find duplicate number.
	
- **Linked list reversal**: 
  - When:
  - Sub-patterns: Reverse entire list, reverse sublist, reverse k-group.
  - Examples:
    - Reverse linked list.
	- Reverse nodes in k-group.
	- Palindrome linked list.
	
- **Topological sort**:
  - When:
  - Sub-patterns: kahn's algorithm, DFS-based topo sort.
  - Examples:
    - Course schedule
	- Alien dictionary
	- Minimum height trees
	
- **Mathematical patterns**:
  - When:
  - Sub-patterns: GCD/LCM, modular arithmetic, combinatorics.
  - Examples:
    - Greatest common divisor
	- Modular exponentiation
	- Pascal's triangle
	
- **Recursion**:
  - When:
  - Sub-patterns:
  - Examples:
    - Divide & conquer (binary search, merge sort)
	- Tree recursion (traversing binary trees)
	- Backtracking (generating permutations, solving mazes)
	- Dynamic programming (top-down) (recursion + memoization)

The other ~10% are often:

- Math-heavy problems (number theory, probability)
- Specialized algorithms (suffix arrays, KMP)
- Domain-specific (low-level systems, graphics programming…)

I can map each pattern to 2–3 canonical problems so you’d have a training set that hits all the main scenarios. That’s how you get from “knowing patterns” to “recognizing them instantly.”





