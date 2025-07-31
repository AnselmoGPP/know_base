# Cracking the coding interview (synthesis)


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
  * [C and C++](#c-and-c++)
  * [Java](#java)
  * [Databases](#databases)
  * [Threads and Locks](#threads-and-locks)
  * [Moderate](#moderate)
  * [Hard](#hard)


## References

- Gayle Laakmann McDowell (2015) ***Cracking the coding interview***, 6th ed. CareerCup.


## Introduction


### Interview process

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


### Behind the scenes

Once you are **selected** for an interview, you usually go through a **screening interview**, which often involves coding and algorithm questions. You typically do 1 or 2 screening interviews before being brought on-site. In an **on-site interview** round you usually have 3-6 in-person interviews. One of them is usually not technical, and the interviewer may not even submit feedback (you can discuss your interests and ask about the company culture). The other interviews will be mostly technical and will involve a combination of coding, algorithm, design/architecture, and behavioural/experience questions. After your interview, your interviewers will provide feedback. Depending on the company, the **final decision** is made by your interviewers, a hiring manager, or a hiring committee. Most companies get back after about a week with next steps (offer, rejection, further interviews, or update). If you waited more than a week, you should follow up with your recruiter. Not receiving an answer indicates nothing about your status. Delays can and do happen.

**Microsoft:** It wants smart people passionate about technology. You'll show up at Microsoft in the morning and fill some paperwork. You'll have a short interview with a recruiter just to ease you. You'll do 4-5 interviews, often with 2 different teams. You'll meet the interviewers in their office. After completing the interviews with a team, you might speak with a hiring manager, which likely means that you passed the interviews with a team and it's now down to his decision. You might get a decision that day or in a week.

**Amazon:** It cares a lot about scalability and object-oriented design. It begins with a phone screen where an specific team interviews you. You will have to write simple code via a shared document editor, and answer questions about the technologies you know. Not often, you may have 2 or more interviews, which might indicate that one interviewer wasn't convinced or that you were considered for another team/profile. Next, you go to the office for 4-5 interviews with 1-2 teams where you will code on a whiteboard and show other skills. The recruiter usually follow up with you within a week.

**Google:** It cares about designing scalable systems, and analytical (algorithm) skills (regardless of experience). It begins with a phone screen, so expect tough technical questions which may involve coding. In the on-site interview you'll interview with 4-6 people. Feedback (based on analytical skills, coding, experience, and communication) is submitted to a hiring committee and managers to make a final recommendation. Making an offer can take several weeks because your packet goes through many stages and committees.

**Apple:** It looks for excellent technical skills, and passion for the position and the company. You should be familiar with the system. You usually start with a recruiter phone screen to know your skills, followed up by a series of technical phone screens with team members. Then, on-campus you will have 6-8 interviews with team members (including your future manager) and collaborators. You'll code on a whiteboard, so communicate your thoughts clearly. The final interview is with the director and the VP of the organization you're applying to. Your recruiter will usually follow up a few days later.

**Facebook:** It wants passionate people with entrepreneurial spirit that love building stuff fast and can hack elegant and scalable solution. It interviews developers for the company, not for specific teams. Once hired, you go through a 6-week "bootcamp". It begins with 1-2 technical phone screens involving coding. Then, you might get homework assignment involving coding and algorithms (care about coding style and peer review). In the on-site interviews, each interviewers has a role (behavioural, coding and algorithms, design/architecture). At the end, your interviewing team and a hiring manager discuss and submit a recommendation to the hiring committee.

**Palantir:** It looks for brilliant engineers. It interviews for a specific team. Usually you get 2 technical phone interviews of 30-45 minutes covering prior experience and algorithms. You might get a HackerRank coding assessment. Then, you will interview on-campus with up to 5 people covering prior experience, domain knowledge, data structures and algorithms, and system design. After this, interviewers discuss with the hiring manager.


### Special situations

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


### Before the interview

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


### Behavioural questions

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


### Big O

#### Time complexity

**Big O time**, or **asymptotic runtime**, is the language and metric to describe the efficiency of algorithms. Most common runtimes are: O(1), O(n), O(log n), O(n log n), O(n), O(n<sup>2</sup>), and O(2<sup>n</sup>).

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

#### Space complexity

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

#### Drop the constants

It's possible for O(n) code to run faster than O(1) for specific inputs. Big O just describes the rate of increase. Thus, we drop the constants in runtime. An algorithm described as O(2n) is actually O(n). Not doing this doesn't make you more precise. Big O express how runtime scales, which doesn't mean that O(n) is always better than O(n<sup>2</sup>).

#### Drop non-dominant terms

Examples:

- O(n<sup>2</sup> + n) → O(n<sup>2</sup>)
- O(n<sup>2</sup> + n<sup>2</sup>) → O(n<sup>2</sup>)
- O(n + log n) → O(n)
- O(5·2<sup>n</sup> + 1000 n<sup>100</sup>) → O(n<sup>2</sup>)

We might still have sum in a runtime. For example, O(B<sup>2</sup> + A) cannot be reduced (without special knowledge of A and B).

Rates of increase of common big O times:

<br>![design patterns table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/rates_of_increase.png)

#### Multi-part algorithms: Add vs. Multiply

If your algorithm has 2 steps, you have to add or multiply the runtimes.

- Add (O(A+B)): Do A first and, when you are done, do B.
- Multiply (O(A·B)): Do B for each time you do A.

#### Amortized time

A dynamically resizing array (`std::vector`) is an array whose capacity increases as you insert elements. When it hits capacity, it creates a new array with double the capacity and copy all elements over to the new array. Describing the runtime of insertion here is tricky. It usually takes O(1) time, but sometimes (when the array is full) it takes O(n).

**Amortized time** takes both situations into account. It describe situations where a worst case happens every once in a while, but once it happens, it won't happen again for so long that the cost is "amortized".

In a dynamic array we double capacity when the array size is a power of 2. After X elements, we double capacity at array sizes 1, 2, 4, 8, 16, … X. This doubling takes, respectively, 1, 2, 4, 8, 16, 32, 64, … X copies.

- 1 + 2 + 4 + 8 + 16 + … + X  =  X + X/2 + X/4 + X/8 + … 1  =  ~2X

Therefore, X insertions take O(2X) time. The amortized time for each insertion is O(1).

#### Log n runtimes

When the number of elements in the problem space gets halved each time, that will likely be O(log n) runtime.

- log<sub>2</sub>X = Exponent of a power of 2 that values X.
  - 2<sup>B</sup> = A
  - log<sub>2</sub>A = B

Example: In a balanced binary search we look for x in an n-element sorted array. We first compare x to the array midpoint. If `x == middle`, we return. If `x < middle`, we search on the left side of the array. If `x > middle`, we search on the right side. We start off with an n-element array to search. After one step, we're down to n/2, then n/4, and so on. We cut the problem space in half each time. We stop when we find the value or we're down to just one element. This search takes O(log n) time.

What is the base of the log? It doesn't matter for the purposes of big O because logs of different bases are only different by a constant factor.

#### Recursive runtimes

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

#### Examples

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


### Technical questions

#### How to prepare

Just reading problems and its solutions whon't help much. You've to practice solving problems. For each problem:

- Try to solve it on your own, and think about space and time efficiency.
- Write the code on paper. This doesn't offer special tools (syntax highlighting, code completion, quick debugging…) and makes writing/editing code slow.
- Test your code on paper (general cases, base cases, error cases…).
- Type your paper code as-is into a computer. Make a list of all the errors you make so you can keep them in mind.

Try to do as many mock interviews as possible with. You and a friend can take turns giving each other interviews. He can walk you through a coding/algorithm problem, and you can learn a lot from experiencing what it's like to be an interviewer.

#### What you need to know

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
 
#### Problem walkthrough

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

#### Optimize & solve technique: BUD (Bottlenecks, Unnecessary work, Duplicated work)

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

#### Optimize & solve technique: DIY (Do It Yourself)

Given an actual example, our intuition can give us a very nice algorithm (somebody that knows nothing about binary search still can use a dictionary book and lookup a word very quickly). Thus, when you get a question, try just working it through intuitively on a real example. Often a bigger example will be easier.



















#### Optimize & solve technique: Simplify and Generalize
#### Optimize & solve technique: Base case and Build
#### Optimize & solve technique: Data structure brainstorm
#### Best Conceivable Runtime (BCR)
#### Handling incorrect answers
#### When you've heard a question before
#### The "perfect" language for interviews
#### Good coding






### The offer and beyond

#### Handling offers and rejection
#### Evaluating the offer
#### Negotiation
#### On the job





## Interview questions

### Arrays and Strings

### Linked lists

### Stacks and Queues

### Trees and Graphs

### Bit manipulation

### Math and Logic puzzles

### Object oriented design

### Recursion and Dynamic programming

### System design and Scalability

### Sorting and Searching

### C and C++

### Java

### Databases

### Threads and Locks

### Moderate

### Hard


Symbols: ≤, ≥, ≠, ≈, √, ∑, →, ↔, ∨, ∧, ~, ¬, ∀, ∃, ⌊⌋, ⌈⌉, <sub>i</sub>, <sup>i</sup>, ∞, Ω, Θ, …
