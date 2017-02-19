---
layout: post
title:  "The Importance of Imitation"
date:   2017-02-19 06:44:23 +0000
categories: jekyll update
---

Today, for my first blogpost, I would like to talk about some topics that have pervaded my thoughts for the past few years -- human learning, machine learning, and Japan. And I'm going to try to do so without using math or too many technical terms.

### AlphaGo

Most people reading this are probably aware of AlphaGo, the Go-playing program based on deep neural networks and reinforcement learning which currently has an ELO (relative skill rating) higher than any human player. A very rough idea of how AlphaGo works is that it first studies many professional games until it has a good idea of where pros will play in certain positions. It then refines the strategy (called a "policy" in reinforcement learning literature) that it learned through an iterative process, in which it plays against a slightly weaker version of itself, and then updates its policy based on whether it won or lost, many millions of times. This high level overview, that the best Go program learned first through imitation, then through refinement, is incredibly important.

What if AlphaGo had skipped the imitation, and went straight to learning by playing against itself with what is essentially a "random policy?" [<a href="ref1">1</a>] Well, the two versions of AlphaGo would square off against each other, each playing horrible, horrible moves. The game would eventually conclude, and then AlphaGo's policy would be updated based on who won and who lost. The issue here, however, is that we don't actually want to increase the probability of these horrible moves. And you might be thinking to yourself, "but if it does this for a <i>really</i> long time, wouldn't it eventually become as powerful as the AlphaGo which started by imitating pros?" That answer depends on how AlphaGo explores the space of strategies, but with the current state-of-the-art in this field (policy optimization), the answer is, "almost certainly no." The learning method employed in AlphaGo is a policy gradient method, which is essentially training a deep neural network which takes a board as input and outputs the best move (for a more technical overview see this wonderful blogpost). This method is good at fine-tuning the strategy from which it starts, but for such a difficult problem, if you start with a trash strategy, you will end up with finely-tuned trash. What I am trying to say here is that starting from imitation not only saves you time when you are solving the problem, but sometimes it turns out to be an essential step.

### Humans do something like this too

I'm not just talking about computers. Even Isaac Newton had once said, "If I have seen further, it is by standing on the shoulders of giants." For a more personal antecdote, when I turned 16 years old, I started to learn how to drive. The first time I was on the road, I asked my father in the passenger's seat, "is it ok to turn here?" He responded, "I don't know, you tell me." My father was a brave man. I, however, was not, and I never ended up getting my license.

But could I have learned how to drive by trial and error, without extra "first-person" human supervision? Humans, unlike current reinforcement learning algorithms, are good at building an internal model of how driving works, even having just watched others drive. While more supervision can never hurt, especially in the early stages of learning, I probably could have successfully learned without getting into a major accident. One of the major reasons that we do not all own self-driving cars right now is that computers cannot automatically build up this model of how the world works. If a self-driving car could accurately predict consequences of actions without executing them (i.e. it has its own imagination), we would most likely have what is called "level 5 autonomy," which is the level at which self-driving cars would be so safe that it would be insane not to use them 100% of the time. Incidentally, even without being able to create this model, self-driving cars are already much safer than human drivers in many situations, particularly in urban and highway driving with good weather conditions. But with the current state-of-the-art, first the self-driving car must learn how to imitate humans from a first-person perspective, then refine what it learned by driving millions of miles in simulation, crashing many times along the way, just like AlphaGo had to lose against itself many times until it learned what was a good move and what was a bad move. Good thing humans don't have to crash a car millions of times before they can avoid it.

As a side note, is there a machine learning algorithm that can learn like a human does (or possibly better)? Yes, there is, even though we haven't discovered it yet. The proof is right in your head. Even though brains are made of meat and computers are made of silicon, there is no reason why the algorithms employed must be fundamentally different. On the contrary, this is a good argument for why computers should eventually overtake humans in intelligence -- because they can use similar or better algorithms, but are not bound to the same constraints that we are (amount of hardware, material used, etc).

### Imitation, Japan, and Korea

Now back to the main topic, imitation. Before coming to Oxford, I lived in Japan for two years. I love Japan very much, but I also have to worry about Japan's future. As many people know, Japan is currently faced with an aging population, and a shortage of children, which could eventually leave the available workforce too small to support the population. The generally proposed solutions are:

1) major reform leading to a better work-life balance, and therefore hopefully more children,

2) immigration, or

3) robots

Anyone familiar with Japan knows that the first two options are not likely to happen, so having intelligent robots run the economy and care for the elderly is by far the most attractive option. Indeed, I went to Japan with the intention of helping them create robots, which is the most practical application of reinforcement learning, at least in the near future. But the employees in the company which I had joined, SoftBank Robotics, had skipped the "imitation" step when learning how to create AI. They read no textbooks, no research papers. They were trying to do everything through brute force, hiring tens of people to write long, brittle programs filled with if-statements, hoping to cover every single case. They tried to build a Japanese chatbot in this fashion. When the CTO would demo it to people, he would hand them a list of sentences and say, "Pepper (the robot) can only respond to these sentences. Say one of them." As it turns out, this isn't how conversations work, and just try building a system like this for many different languages. (Nota bene, the CTO also said that machine learning was "an American joke" and that it doesn't exist, but that is a story for another time)

Even had SoftBank been imitating current research with no research or innovation of their own at all, as most companies actually do, they probably would have been able to push out a decent product. So why didn't they do it? Well for one, they couldn't read the research papers. Any paper worth reading is published in English and, well, none of my coworkers could read English very efficiently or accurately. But this problem extends well beyond academia, and lack of English isn't entirely to blame:

<div style="position:relative;height:0;padding-bottom:56.25%"><iframe src="https://www.youtube.com/embed/41Dp7Q-SM1Y?ecver=2" width="640" height="360" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>

This is a K-pop song that came out four days ago. If they weren't singing in Korean, this could easily be on American radio. Actually, I personally think this song is better than most American pop songs, but I am most likely biased. The point I am trying to make is that while Japan flounders with trial and error, not properly exploring the space of strategies and settling on undesirable local minima, Korea has taken to heart the "imitate and then refine" paradigm, and this has pervaded every aspect of life, from music, to school, to research. And I believe that Korea will benefit greatly from this, while Japan is shooting itself in the foot. At the very least, their music industry is reaping the benefits of having "imitated and refined" American pop.

<div class="imgcap">
<img src="/assets/someta.png">
<div class="thecap">Korean researchers, who have mastered the "imitate and refine" paradigm, learning from other researchers by imitating their imitation learning papers #someta</div>
</div>


I used to think that Japan would be served well by learning more about recent advances in AI, but after having lived and worked there, I think its problems are more basic. What I think Japan needs more than anything else is to learn how to learn, and that begins with learning how to imitate.

==

<div id="ref1">
In the days when Sussman was a novice, Minsky once came to him as he sat hacking at the PDP-6.

"What are you doing?", asked Minsky.

"I am training a randomly wired neural net to play Tic-tac-toe", Sussman replied.

"Why is the net wired randomly?", asked Minsky.

"I do not want it to have any preconceptions of how to play", Sussman said.

Minsky then shut his eyes.

"Why do you close your eyes?" Sussman asked his teacher.

"So that the room will be empty."

At that moment, Sussman was enlightened.
<div>
