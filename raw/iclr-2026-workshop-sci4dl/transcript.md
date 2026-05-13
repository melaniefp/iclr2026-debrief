# Workshop Transcript: Scientific Methods for Understanding Deep Learning (Sci4DL)

> Auto-generated from video subtitles. Timestamps reference the workshop livestream.

**[00:25:21]** Or for any realistic deep learning setting. I'm claiming. On the left, I'm gonna plot the train loss, and on the right, I'm gonna plot the top eigenvalue of the Hessian. So let's start training. And as we train, we can see the loss goes down and the sharpness goes up. Now we don't know why the sharpness is going up.

**[00:25:46]** This is still unexplained. It seems to be a very robust property of deep learning objectives. But the sharpness goes up. And at some point, gradient descent leaves the stable region. And so at this point, there's now a direction in weight space that's too sharp for our current learning rate. And we know that on a quadratic, like on the local quadratic Taylor approximation, grading descent would oscillate and blow up.

**[00:26:12]** So the question is, what's gonna happen? On the on the real objective? Okay. So let's run gradient descent for the next several steps. And on the right, I'm gonna plot Zero. From along the top eigenvector of the Hessian. From, like, measured relative to, like, the start of this animation. So it's just this quantity. We'll

**[00:26:42]** use the u t zero as the top eigenvector. This is like the thing that we, expect to oscillate. According to our local quadratic model. Okay. So let me start running. And we can see that we we are indeed oscillating along the top eigenvector. As one would expect. So we're doing this along the highest curvature direction. And the oscillations start small, but

**[00:27:10]** they eventually get because they're growing exponentially, they eventually get so big that the train loss starts to go up rather than down. Which is not good. And so the question is, what's gonna happen next? Is training gonna succeed? If so, it's not clear how it can succeed. Because remember, as long as the sharpness is above this, two over eight line, we expect the oscillations along the top I conjecture

**[00:27:36]** to keep growing exponentially. So it's not clear how things are gonna stay okay. So let's see what happens next. I'm gonna run for several more iterations. So what's happened? The sharpness has dropped. Which is very nice because that's just what we needed to happen. And once and in in fact, the sharpness

**[00:28:06]** falls all the way below two of her ADA. A. Once the sharpness goes below two over eight a, dynamics along the top eigenvector become contractive. Again, that makes sense. And the loss comes back down. That also makes sense because those we both expect from like a local quadratic story. The question though is why did the sharpness drop just when we needed it to? Did we get lucky?

**[00:28:31]** Is this something we can expect? So that was just the beginning of the trajectory. Now let me show the full trajectory of gradient descent. So the sharpness goes up to two over e dah. And then after it reaches two over eight, it stops going up further and instead equilibrates around that value. Meanwhile, the losses going down over the long run but it's behaving non monotonically

**[00:28:54]** over the short run. Let's try different learning rate. That was learning rate o point o two. Let's now try a learning rate of half that size, o point o one. So in orange, I've drawn the new two over ADA. And we see that the same thing happens. So the sharpness goes up to new two of her Ada, and then equilibrates there. So in other words, to go back to the beginning, if the expectation

**[00:29:21]** is that gradient descent is starting and remaining inside the stable region, the reality seems to be that it's actually tending to leave the stable region but whenever it leaves, it somehow steers itself back inside. So how is that happening? We call this training at the edge of stability.

**[00:29:45]** So and this behavior is not specific to that particular network and data set, Rather, I'm claiming that this is the typical behavior of gradient descent in deep learning. So here I'm showing you three image tasks. Three three image architectures on an image task. You see the same thing is happening. Here, I'm showing you, three sequence architectures

**[00:30:09]** on a sequence task. Same thing's happening. So I'm not saying oh, wow, if you like set up things in this weird way, this is some weird edge case that you can force. Rather, I'm saying that this is the typical behavior of gradient descent. Now, when I say gradient descent, I mean gradient descent. And the reason why your runs don't look exactly like this because you're not using gradient descent. You're using maybe stochastic

**[00:30:33]** gradient descent, or Adam, or now muon. But what I'm claiming is if you used gradient descent as the optimizer, but kept everything else the same, this is what your training would look like. That's what I'm claiming. So the question is, what's going on? We ask this question in our paper several years ago, Why is gradient descent working if not for any reason we can find in the literature on optimization?

**[00:30:58]** So the answer, in my in my opinion, a great answer was given by the subsequent paper, by Alex Damien, Ashaun Nachani, and Jason Lee. And what they pointed out is this, to understand the dynamics that we just saw, all you need to do is tailor expand to one order higher. Than is normally used when analyzing

**[00:31:23]** first order methods. That's it. So this tailor expansion so we're gonna need to tailor expand a third order in the loss. So this Taylor expansion reveals the crucial ingredient that's missing from current optimization theory. Without this ingredient, you can't understand the behavior of gradient descent. In deep learning. With it, you can. The key fact is that oscillations

**[00:31:46]** along the top eigenvector of the Hessian automatically induce reduction the top eigenvalue of the Hessian. So let's let me sketch that informally. You can see their paper for a more formal treatment. So suppose we're moving through weight space and we're oscillating along the top eigenvector of the Hessian. Which is like the vertical direction here. So let w star

**[00:32:10]** denote the point where you'd be if we if we were not oscillating. And let w denote the point where you'd be where we are because we are oscillating. So in other words, because we're oscillating, we're displaced from w star along the u direction by some magnitude. Let's call that x. So how does the gradient where we are w star plus x u, relate to the gradient at w star is

**[00:32:35]** where we'd be if we were not oscillating. So by Taylor expand let's let's do Taylor expansion. Gonna tailor expand Noblal the gradient map around w star. So okay. First term is not very interesting, just gradient w star. Next term, which is first order in the gradient or second order in the loss, says that the gradient w star plus x u has a term that

**[00:32:59]** is like Hessian at w star, times x u. That should make sense because the Heshn is the derivative of the gradient. But we can simplify that further because u is an eigenvector of the Hessian, particular, it's an eigen value eigenvector whose eigenvalue is s, the sharpness, So Heshin times u is just sharpness times u. And sharpness is a scalar. So this is a

**[00:33:23]** vector that's pointing in the u direction. And when we follow the negative gradient, this term's gonna send us into the minus u direction. So this is just the term that's causing the oscillations. As we already expected The magic quote unquote, is coming from the next term, in the Taylor expansion of the gradient. So the next term looks like this, me unpack

**[00:33:45]** it. This is the curvature in the u direction. U transpose hessian u. This is the gradient of that. So the gradient of the curvature in the u direction. The curvature in the u direction well, because you as a top eigenvector of the Hessian, this is just the top eigenvalue of the Hessian. Or the sharpness. And moreover, you can show that the grading of the curvature

**[00:34:07]** e, e, direction, is just the gradient of the sharpness. In other words, just by tailor expanding, we see that the gradient at w star plus x u contains the term that is proportional to the grading of the sharpness. Thus, when we take a negative gradient step at w star plus x u, it's gonna automatically take

**[00:34:30]** a negative gradient step on the sharpness. And the step size, quote unquote, of this negative gradient step is one half eta x squared where remember that x squared is the squared magnitude of the oscillation. So the larger the oscillation, the stronger the implicit gradient step on the sharpness. So in other words, we already knew that sharpness generates oscillations. But

**[00:34:55]** now what we see from this third order expansion is that there's also an arrow in the other direction, where oscillations reduce sharpness. So you can think of this as a negative feedback loop. Yeah. When the sharpness exceeds two over eight, grading descent oscillates along the top eigenvector, but in turn, those oscillations automatically perform gradient descent on the sharpness. Thereby allowing gradient descent

**[00:35:20]** to automatically remain inside the stable region. So let me revisit the behavior of gradient descent that we saw before. So initially, when the sharpness is bigger than two of VARTA, that leads to exponentially growing oscillations. But in turn, the oscillations implicitly take negative gradient steps on the sharpness pushing the sharpness down. These two things are coupled.

**[00:35:48]** And if you want to analyze gradient descent, you go and analyze that coupling. Okay. Out for time. Oh, wow. I have more time than I was expecting. We, so this was full batch grading descent. But, similar behavior has been shown for other optimizers in the full batch setting. Including Adam, for example,

**[00:36:18]** if you wanna see the next step is to analyze these dynamics. And if you're curious about that, we have this paper understanding optimization in deep learning with central flows. Which we we wrote last year And, I recommend the blog post version of that. We've got some animations there.

**[00:36:47]** And finally, this was all talking about full batch gradient descent, which is not realistic, but this is a special case of a more general thing holds for SGD. And we're working on that currently, and we'll put out a paper on that soon, hopefully. Okay. So so what? How does this suggest a better algorithm?

**[00:37:14]** So that's a some people's reaction. So in response, I would say that's not our immediate goal. Our our our thinking is that practical algorithm design in deep learning is not currently bottlenecked on people working to apply known principles, rather the barriers that are principles that we don't know. And that's the bottleneck.

**[00:37:40]** And so we think the reason why we've been working on this direction is that we think that the way to maximize our long term impact on practice to focus now on understanding the foundations so that later, we or others can apply that understanding to make practical algorithms that work effectively. So maybe someone will put this theory to good use next month, or maybe it will take a

**[00:38:06]** long time. Either way, we have faith that eventually, a true understanding will yield practical gains. And perhaps big ones. So if I could make a, broader point about the field, I I I I feel like most people in ML would say that the platonic ideal of an ML paper goes something like, oh, first you identify

**[00:38:33]** some insight, then you formalize that insight into a theorem, and then you leverage that that insight and that theorem to obtain a new a new algorithm. That gets you know, it's is the bold figure in the table. That's sort of the Platonic ideal of a machine learning paper. And when I see a paper like that, like a lot of the time my reaction is like,

**[00:38:59]** like I I think to myself like, either like the theory is sort of like exaggerated, or the experiments are exaggerated, or both are exaggerated. So I think that the field of ML I don't think it's currently possible in most cases to design principled algorithms that really work well in practice. The problem

**[00:39:23]** is we just don't yet know what the principles are. I think that the field sort of has this collective action problem, so to speak, where like, the official standard that everybody holds themselves to is not really attainable. In practice. Like it's not really because we don't know what the principles are, you can't really have a work where you you know, theorem

**[00:39:50]** plus like like plus soda equals theorem plus algorithm equals soda. And so I would say that it's better to sort of do something more modest in scope but but do it well, than to try to do too much. And so, I think that, like, the field would be a lot healthier if there were less of an insistence on for example, theorems instead we

**[00:40:15]** should focus on understanding and then the rigor will arrive gradually over time. And similarly, I think it's too ambitious to focus every paper on trying to you know, develop a state of VR algorithm, we should instead focus on understanding with the faith that true understanding will improve the practice. In the course of time. Finally, I wanna highlight

**[00:40:39]** a great paper that, Jamie Simon, Dan Dan Coonan, and others have put out recently. I also help with this. Called like there will be a scientific theory of deep learning. Just containing some promising directions in this area. And you should also check out this website, learningmechanics.pub,

**[00:41:03]** which is gonna be a it's gonna have, blog posts on, topics in the theory of deep learning. So I just wanted to call that okay. Thanks. And all the questions. Thank you, Jeremy. That was, fantastic. So if you have questions, you can go to this mic at the front, or you can also just raise your hand. And

**[00:41:38]** then I will come to you with the mic. So maybe to get started, Jeremy, I'm sure you have some thoughts on what kind of loss landscapes would drive the would lead the gradient descent to drive sharpness up because of course for quadratic objectives, this doesn't happen. So, like Yeah. So that's one of the big remaining like one of the big open questions like, why does this why does the sharpness tend to want to go up?

**[00:42:03]** I mean, I think the heuristic answer that a lot of people have is that sharpness is something is correlated with something like complexity, and so gradient descent is trying to make the function more complex. As it fits the dataset. But that's just a hand waving notion. So I I think it's still, open problem. Cool. Thanks. Yes, please.

**[00:42:27]** Yeah. Thanks for the nice talk. I can hear me from here? Yeah. Cool. I have, like, kind of a simplistic takeaway, and I'm wondering if you can disabuse me of it. It seems like the when you're in the weight space that induces oscillations, well, as you've said, it's unstable. And so I think, well, that kind of explains itself a way that it's it's unstable, so you would leave that region. But

**[00:42:50]** why don't I just say something more nuanced? But I'm wondering I can just kind of keep that in mind. But you leave the region, but then why should something why shouldn't you just blow up? Why should you leave the region to a region where the sharpness is lower rather than the region where it's higher? Yeah. I guess just in the sense that you, like, leave anywhere that's unstable. And then the question is, like, how common are unstable for

**[00:43:12]** stable regions? But the the key point is that, like, I'm not saying that I'm saying when you look at this third order expansion, it's not that like, okay. Let me sorry. Let me go back. I don't think I did this very well. The So suppose we were, suppose we're at this point. So go back to here. Like, the things don't look so good. Oh,

**[00:43:54]** yeah. We've started to blow up. Things don't look very good. Let's say you wanted to fix the issue manually. Right? So the what is the issue? The issue is that the sharpness is too high. So the most natural way to fix the problem like, the sharpness is is high enough that, like, locally, like on our local quadratic model, we're gonna blow up. And so, the

**[00:44:18]** most natural way to fix the problem would be okay, if the sharpness is too high, Let's move to a region where the sharpness It it automatically picks up that grade that that grading of sharpness term. Yeah. That was the third order of Heather. Yeah. Yeah. Yeah. So I'm not Yeah. So I'm not saying that the third order term is like empirically something that we observe to be aligned, like, aligned with the negative gradient, the sharpness.

**[00:44:43]** I'm saying it is the it is the negative gradient of the sharpness. So it always gives us like the the stabilizing effect that we need. So I guess I should take away from that. There's, like, something even more precise than my intuition. So Yeah. Yeah. Yeah. Thanks for that. Thanks. Do we have, more questions? Yes. Yeah. Thank you for your talk. When I

**[00:45:12]** see the loss like that, when the loss explodes Yeah. I Mhmm. And why the loss returns to the same low loss region? Why model recovers after the blow up? Yeah. Great question. So it's because we were just bad along one direction. Like, the loss was only high because we were, we were blowing up along this one particular direction, the top eigenvector direction.

**[00:45:37]** And so once we once the curvature in that direction shrinks and you you contract it getting along that direction, like, you you gain back all the progress that you had apparently lost. So it was like let me put it another way, like, even when the loss was so high, like the loss is high here now, if you look at the average between like two consecutive you take two consecutive iterates and you look at the midpoint between them, the loss there is like not

**[00:45:59]** bad. Like the spike only does that make sense? Like if you were to pair average successive iterates, that trajectory doesn't have a big spike. Like, you're only getting the spike because you're doing it's literally just because you're doing like this along one direction. How you should think of things. You're good in all the other directions, but you're doing this along one direction. Okay. Okay. Yeah. Thank you.

**[00:46:27]** Hi. Thank you very much for your talk. Looks to me that this oscillation is making you climb up the your local convex region. Right? Yeah. Your optimization space might be very regular. This might be helping you to reach other convex regions that have better local minimals. It's a good Yeah. It's a good question. So originally, like, that was how like,

**[00:46:51]** that seemed like to be a reasonable way to think think of things. Our latest understanding is that it's it's not good to think of things as like transiting between it's it's not like gradients and it's transiting transiting between like distinct, like, discrete regions. Mhmm. Like, instead like, what we what we argue in this this sort of what we show in this, like, more recent paper is that this whole time, when it's at the

**[00:47:14]** edge of stability, it's effectively following this this other differential equation. So it it doesn't follow, like ordinarily, gradient descent follows the gradient flow, but when it's at edge stability, it follows like a different differential equation. But so everything I I don't think of like, the like, the oscillations mostly cancel out. And there's this like smooth underlying picture. I see. I Yeah. I don't think of it as distinct

**[00:47:40]** regions, even though that is a natural way to think about it. And would it be possible to map these, convex regions and check if you are actually jumping between them? Or just staying the same. It's not like I I don't know the answer. Yeah. I don't think it's Yeah. I don't think of it as being jumping between like, let me okay. Let me go back to this picture. Oh, Like, if if you go back to this

**[00:48:13]** picture, like, what, we go you see where we go out of the stable set, and we get back in. Mhmm. You could have affected it's basically doing the same thing as just going to the border of stable set and then just staying there. So, like, the that's, like, the big picture takeaway. That, like, you should think of Grey Newsom as like moving to the border of this table set. And then implicitly, it's projecting out the components of the gradient

**[00:48:40]** that would bring us out of the stable set. I I didn't get to that in this talk, but that's the the right big picture takeaway. Okay. Thank you. Thank you. Yes. Maybe one more question. This last picture got me thinking like, if the stable vision is pretty wide, but why we always follow the one really narrow reach region of that

**[00:49:04]** stable? Region. And you think it's get some, similarity with the platonic manifolds? Like, that all basically models if they trained long enough arrive to a similar minimum. I don't think I don't think there's a Could you repeat So the second half of the question I don't think there's a connection,

**[00:49:27]** but I I haven't looked into it. The first half of could you clarify the first first part of the question again? Yeah. So this picture got me thinking that if we always follow the just the edge of the stable region Mhmm. We basically not exploring all of the different possibilities in the white space. Yeah. Good question. But it's the the landscape is so overparameterized

**[00:49:51]** that there are like good Well, okay. If the learning rate is too high, you can construct you can definitely construct tasks where the learning rate is so high enough that you can't even solve the problem within the stable region. And you can't get zero error. Is your loss. That is a possibility, but it's not it doesn't happen. Most you can definitely construct examples where that

**[00:50:12]** holds, but in practice, this table region contains like zero loss solutions. Just because there's the weight space is I the big hand wavy justifications of the weight space is so high dimensional that you can it's like overparameters that you can find a good solution even in there. Alright. Makes sense. Thanks. Okay. Let's thank Jeremy again for a great talk.

**[00:50:40]** Our next speaker is, Julian Campe. Julia is a silver professor of computer science, mathematics, and data science at, New York University. And she's currently on leave at Meta Fair in Paris, where she's a senior scientist and director of the foundations of reasoning team. And Julia is known for very high quality

**[00:51:04]** contributions to adversarial robustness, model collapse and journey models, and more recently reasoning in LLMs. And she also had previous lives in quantity finance at Renaissance, and in, quantum computing and information. And we're, very excited to have a have her here. And let's welcome her with a round of applause. Yes. Hi. Can you hear me? Is it good?

**[00:51:35]** So thank you for the organizers for getting us to this wonderful location. It's a real pleasure to be here in this workshop. What I want to talk about today is, so switching a bit, topics, We're going to speak about LLM reasoning, and trying to understand some phenomena that we are have all heard about. My talk will basically be based on

**[00:52:00]** let me see if I can get this better. Will be based on two papers One spearheaded by my student, Nikos, there on the top row, with Iran and Karen, And another one that was done at Meta, with fantastic intern, Shobita. And colleagues at Meta. So, let me give you a little

**[00:52:23]** bit of, you know, brief history of LLMs, and we're gonna start right, in 2020 or slightly pre 2020. Maybe you recall we had GPT two, and the paradigm that emerged at the time was let's pretrain this LLM, and then let's fine tune it to wherever we want it to go. You know, new summarization or something else. That was the paradigm.

**[00:52:49]** And then around 2020, these are all kind of empirics, right, that appeared. People realized that these pre trained next token prediction, pre trained LLMs are fantastic in context learn learners. There was a whole flurry of the community trying to understand what's happening in context, beautiful work was done also theoretically to understand what is the mechanism behind this in context

**[00:53:13]** learning. And then, in 2022, I would say, this one in one of these papers, let's think step by step. There was this new revolution where when you tell the LLM, you just think a bit, suddenly it became a much better performer and also, in particular, a much better reasoner. Right? And, again, there is a lot to understand here. And for our community, to kind of try to isolate the mechanism

**[00:53:38]** of what's happening. So, this is pre history. And then, about a year and a bit ago, we had the appearance of these so called reasoning models, I think the first one maybe that we can pin down is o one, followed very quickly by Deepseak and Kimmy, where, there was a new kind of training or post training paradigm which is now called RLBF,

**[00:54:03]** reinforcement learning with verifiable rewards. Which led to fantastic, you know, progress in coding and math and all these, verifiable domains, also in science, basic So, this is interesting because there's a lot to understand here. And just, stepping forward because people keep asking me what's now, think what most of us observe now is yet another phase transition where we

**[00:54:27]** start to have several agents, API access to powerful foundation models, that we make interact. Right? And, there's fantastic new territory scientifically to understand there is now, instead of in weights RL, there's maybe in context RL or in skill learning, all these new things are happening, and I'll try to allude to them. But, let me focus on stuff

**[00:54:50]** that happened about a year ago and what what we try to understand. Okay. So, reinforcement learning for LLM post training, we already had RLHF where we kind of you know, had had responses of the LLM, and then we waited them, we had them annotated, one better, one worse, and we did reinforcement learning. And the kind of reasoning revolution, that started about a year ago, a little more,

**[00:55:14]** was to do this, you know, open AI, as I said, deep sea and Kimmy. Was to do several rollouts, several thinking traces of the LLM, and then, you know, have some sort of group average of the reward and reinforce these thinking traces. And this, mechanism, which is which was called group relative policy optimization and about 500 versions of

**[00:55:37]** it later. I mean, maybe not 500, but many, the paradigm was basically that, as I said, you have these rollouts. Right? A group of multiple chain of thought outputs, say 16, Right? And then, you have a verifier that checks after this long chain of thought the output is and whether it's correct or wrong. And then, the verifier gives a reward, which is often binary. And then some sort of average is computed, and then

**[00:56:00]** everything better than the average gets rewarded, and everything worse. Than the average gets penalized. And this is kind of put back into the loss And restarted. Right? So, this is a this is the the mechanism And, what people observed is, that during that ROVF training, the chain of thought lengths would increase. Right? And you've probably all seen these famous curves

**[00:56:23]** of how how it goes. Up and then also, you know, test time, compute increases, of course, because then the answers have a long chain of thought. And this is all very interesting, but do we understand it and where is it coming from? Right? So this is what we wanted to understand. What does this RLVF actually do? I mean, many people wanted to understand it, but here, I'm gonna present one way to isolate isolate this mechanism. So,

**[00:56:45]** and then also the question that was then, you know, being it's still being discussed in the community is, do we actually learn something, or are we just retrieving something that's in the training data hidden somewhere? Right? So that's the question. And I'm you know, there's a quote by Bubeck in one of the interviews he gave where he says, the intelligent already intelligence already exists in the pre trained model,

**[00:57:07]** it's all about extracting it. And I'm putting it there slightly provocatively because I actually don't believe this is fully true, but there is some truth to this. I think. And that's what our role does. So let's try to understand this a little better. But before we do, there is this other question which, or maybe it's complementary or similar. There were these observations, by many papers, including one of ours,

**[00:57:31]** where we compare the model before it was trained with this RLBF procedure and we we we we look at pass at k pass at higher k rates. So, we ask the model to do a 128 rollouts And if there's one correct one, then we say pass it k as one safe. Instance. And we compare this high pass it k rates with then the post trained RLBF model. When you look at

**[00:57:54]** these number of samples here, you can actually see in some experiments, and again, this this is still being debated. Sometimes it's true. Sometimes it's less true. But you can see that, basically, the RL model, the RLVF model, tends to become sometimes even worse than the base model at pass at higher k. So then, people just say, you know, RLVF does nothing but bring the pass at k.

**[00:58:16]** To the pass at one. But then it becomes less diverse and so on and so forth. Right? So this is also observations people have made. And, there's another paper I like that also appeared about a year ago, by I think, people at Harvard. And also I think mostly people at Harvard. Where they did just a controlled study because it's very hard to study

**[00:58:38]** this we don't have any understanding of what the pretraining data set looks like. Right? I mean, we don't know mean, we do know it's the Internet, but we don't know how the data is curated in the foundation models. They did a study where they just retrained a model from scratch, pretrained it, had a very careful look at the pre training data sets. And what they observed is, let's see. In particular, what they

**[00:59:00]** observe is that our algorithms consistently converge towards a dominant output distribution distribution amplifying patterns in the pre training data. Right? So, they observe it by having different flavors of pre training data, different formatings, etcetera, and they see that RL picks up one of them. For math or whatever. We wanted to understand this a little better. What that means. Right? And so, our

**[00:59:23]** hypothesis here was that in the pre training data, you will have a lot of short data in the sense that there is a question and an answer, something like this. Then occasionally, you have very high quality data where you have a question, then a long explanation, deliberation, thinking trace, then an answer. Right? And, so

**[00:59:47]** what we did in the study is we assumed that when you have a long pattern, then you can generalize pretty well from it. If you know how to think. You have a short pattern, just question answer, you cannot quite, generalize because it's it doesn't reveal the thinking we are making this assumption that that's how the pre training data looks like then we want to understand what RLVF or RL,

**[01:00:09]** gRPO, etcetera, does to this. So, particular, we are asking why is it difficult for a model to generalize if you just do pretraining or just do SFT, next talk and prediction, And what is this thing that RLBF does or our reinforcement learning in general to suddenly get this knowledge out. Right? And why why do the thinking traces then get longer? Right? So, this this was the question we asked.

**[01:00:33]** And so we we wanted to isolate this mechanism and we started with a very controlled experiment And we were lucky that this experiment was devised in such a way that in a slightly simplest setting, we could actually prove everything. We have like a full theory, that matches these experiments. Because they are actually somewhat analyzable. But first, let's let's describe the experiments. So we modeled the pre training data

**[01:00:56]** with a parity problem. Parity, you know, zero one and then the the sum is even or odd. Basically. XOR of or if you wish XOR of the training bits. So we have inputs our training bits, bits, sorry, bit strings. And then in the training data, we have a mixture Either we have, long demonstrations, where we have these bits of input, and then we have these partial parities. You see

**[01:01:20]** this there on the bottom line of this blue yellow red. So, we have the blue input, It's a string of zero ones. And then the yellow bits there are partial parities, so the parity of the first bit, the parity of the first and the second bit, the first second third, and so on. Is how you would compute parity probably. Right? You would go along the chain, compute the partial parities. I mean, how else can you do it? Right? And then, the red is the

**[01:01:42]** output bit. So what we what we'll have is training a training mixture for a small transformer which is a lot of these short answer parities and a a few, a fraction, which we call p of chain of thought, p code, of these long demonstrations. And what you need to know about parity is usually one, you know, in theoretical computer science, it's always used

**[01:02:04]** as prototypical hard problem. It's hard. Parity is not so easy. To do, you know. Whereas, if you have this long chain of thought, and you just follow it along and you reason this way, then it becomes easy. Right? So, this is our training mix. So, we use this dataset that has a lot of these short demonstrations, and some of these longer demonstrations And, our hypothesis is that this is basically

**[01:02:25]** mimicking the Internet we have some step of step reasoning step by step reasoning examples but there there's like, they are drowned in this sea of very short answers. And the noise and so on and so forth. Right? So just we did this experiment. We ran a small transformer on it. And what we observed is that, and we have a next token prediction, I should say. So what we observed is indeed when the transformer kind of starts mimicking the dataset

**[01:02:48]** it's trained on. So, if there is, for instance, 20% long demonstrations, and 80% short, then the transformer will also at the end of training output, 20% long stuff and 80% short stuff. So, it remains length calibrated. If you just do SFT next token prediction, pretraining. We saw it in experiments we could prove this also

**[01:03:12]** theoretically with a with a simplified model. With a, you know, with an ensemble of linear transformers. So, and on the other hand, when it got a long one, so in the 20% of cases where it had a long one, it very quickly learned to generalize. So it generalized meaning to unknown sequences. Right? So, in the test set, we had sequences

**[01:03:36]** of bits that they didn't see that the transformer didn't see in. And, pre training, And, whenever it decided to output a long answer, it was very quickly learning to be correct. But for the short answers, it just, you know, it would have take I mean, it just didn't work. Right? It just was hard a hard problem to learn. So, as a result, when you look, when we did the analysis then, we had like, on the

**[01:04:00]** left side, you see this accuracy for various mixtures of this long demonstrations in the data set. So if there's enough long demonstrations, in fact, there was a threshold at one third, when you have more than a third of good demonstration long demonstrations, and then you do, and then you look at the accuracy, see how quickly it learns to predict the right answer when it answers

**[01:04:23]** with a long demonstration, which will happen, you know, in a good number of cases. And when you do greedy decoding, for instance, which is on the, right side, then there's this threshold of one third. Of the mixture of the pretraining data before, if you if you have less than this, good demonstrations you just have no accuracy. Because in the greedy case, will just always output the short ones.

**[01:04:46]** Because it remains length calibrated. So if it doesn't have a choice, a randomness, will always do the short demonstrations, won't learn anything. Right? It will only guess randomly 50%. But, once you have more than a third, it will learn to output, with higher probability, long demonstrations where it quickly learns. Right? So, all this we observed. And I'm not gonna bore you with the theory, but all this we could literally prove, including

**[01:05:10]** the one third, for our linear transformer with the frozen layer, basically. So so that was nice. So that made us understand why SFT fails, but that was not what we wanted to understand. We wanted to understand what happens with RL. And so now what we did is after we've trooped pre trained this transformer, we now did what RL does. So, good answer, we would reinforce it.

**[01:05:33]** We would say, you know, we would give it a positive reward, whenever there was a wrong answer, we would give it a negative reward. So what happens is whenever it sees a long demonstration, the answer will be correct. Right? Because we had pre trained it. So, the long ones would be picked for, like, being positively rewarded all the time. And for the short ones, only half of them would be correct, So there would

**[01:05:54]** be much less of them picked, only half of So, at every step of this And then we would re retrain the model. Right? I mean, then we would basically reinforce this thing and keep going. So, as a result, we kind of up sample the long ones because they get rewarded much higher probability, namely one, basically. And And as a result, after logarithmically few rounds in the fraction in the lengths, I mean,

**[01:06:16]** in one over the fraction, of the long ones, we get to perfect accuracy and also the length of the chain of thought, of course, increases because it was start outputting only the long chain of thought. And we can see all this here. So, here is this training we have very few long demonstrations, like, say, 20% or 2% or 5%. And we see how we train, and then we switch. So we train

**[01:06:38]** SFT and we get to this 50% but no more because, you know, under greedy decoding, it will just output short things. And then, at some point, we'd stop and do this RL training. And you see how immediately the accuracy just jumps up to nearly a 100%. Right? We RLBF. Procedure, which is exactly what our theory says.

**[01:07:01]** And the length of the chain of thought would increase after we do this, and it takes very few rounds. So, all this we saw in the experiments, in the theory, it was very rewarding for us because basically, we started with the hypothesis that there is some good stuff in the pretraining data, lots of not so good stuff, here's the mechanism by which RL actually you know, zooms into what happens in the

**[01:07:23]** training data. So, here is the length increase, I guess. We we see some sort of, heat map of the length. But, this is all just to reinforce the message that with this parity example, we could explain what's happening in RL. And let me, now summarize the mechanism again. So, during pretraining, what happens is the model quickly learns from the long stuff. But it doesn't increase the long stuff. So, when it sees, when it decides to output

**[01:07:46]** a long chain of thought, knows how to generalize. Right? But, when it decides to output a short chain of sort, it's too hard to learn disparity. It fails to learn. And because it remains length calibrated, it will be wrong a lot of the time if there's very few good samples in the training data. Right? And then, during post training, this RLBF or we we analyze the star algorithm where we just

**[01:08:09]** picked good, you know, positive reward samples and did some SFT on those and iterated this. So, because RL rewards correctness of you know, reward weighted correctness, the the it effectively up samples the long chain of sorts samples of the correct stuff from which it can learn. And shifts the model policy this way. Right? And

**[01:08:31]** then, because this goes so fast, this, you know, this up boot bootstrapping quickly, you can do the calculation, it's really very fast at logarithm one of a P code. Right? So, r l is highly effective to mine and capitalize on rare, high quality examples. Which, you know, which was kind of a wisdom that people already kept repeating, but we were pleased to see this here, And also

**[01:08:54]** the long chain of thought, it's not because, language model needs a scratch pad or anything. It's in this case, it really comes from the optimization pressure of this learning procedure. Alright. And then, because we also wanted the paper to have some relevance, we repeated this in the wild. So, we actually took pre trained LLMs. I think in this case, it was some llama

**[01:09:17]** model. What is it? LLAMA three b. And we did this with GSM. It came with the math data set. We repeated this study. So, either we did the GSMAK with a mixture of no chain of thought and full chain of thought, and we did SFT, and then we did RL, exactly like with the parity, and we see exactly the same phenomenon. Right? So it doesn't learn very much, and the moment we stop and switch to RL, the learning goes up. Like crazy in logarithmic in many

**[01:09:39]** steps. So exactly the same mechanism for pretrained models. So so we were happy that this framework explains something. Alright. Let me switch quickly to a second, problem. So, with ROI, as we saw, with RLBF, what happens is that you during learning, you give it like 16 chances output of chain of thought, and then you'll amplify the

**[01:10:02]** correct answer and penalize the wrong answer. What if the problems are so hard that there is no correct answer in the beginning? Right? So hard with this procedure, where you need something to I mean, you need a signal, you need at least one of them to be correct. Kind of hopeless for hard problems when nothing is correct. Right? I mean, obviously, because because, you need you need to amplify something. So, hard problems cannot be learned,

**[01:10:24]** with ROVF unless you try very, very long time and then randomly some correct answer happens and then you amplify this. Right? So, and and as we said, these current r l recipes also primarily preserve the base model solution coverage. So, it's really kind of a bit doomed with hard problems, and what people have been doing for a long time Oh, let me not people have been doing for a long time is they try to design

**[01:10:47]** curricula. Right? I mean, for these math problems, very hard, Remember, there was first college math was solved with GSMAK, and then high school math, right, with the math data set. And then the IMO, that's only last year, remember? I mean, IMO, Putnam, all these are happening, but it's, there's no coincidence that it goes step by step, so to speak. So there's lots of curriculum design going on, but it's often handcrafted.

**[01:11:11]** Right? So, we try to give it easy problems, medium problems, hard problems. But what if we don't actually know what is easy, medium, and hard? Like, I ask you to solve the Riemann hypothesis, come tell me what's the easiest I mean, what are the stepping stones? We don't know. Right? So if we were ambitious. So how do we automate this curriculum learning and so this is our paper at the edge of learnability. Edge of learnability means you can't learn

**[01:11:33]** it, but then if you're clever, you can learn it. Right? So, we have this plateau, we have no training signal. What do we do? Our LDF will just wander around and not find anything. So, we need this curriculum and it's often done curated data, filter existing data, all these handcrafted ways, but it's either it's not principled or it doesn't work or it has its problems. Right? So the idea here is maybe the LLM

**[01:11:57]** from its huge pretraining set, already kind of knows or has enough easy problems Right? Riemann hypothesis. It has read all the papers on the archive. Maybe there is a curriculum of stepping stone math results to the Riemann hypothesis We just don't know it. I mean, I'm being ambitious here. Okay. So, let the LLM itself decide what is its curriculum. This is the idea of the self play and self improvement. And

**[01:12:20]** so, we designed one such procedure. This is this is an experimental result, and we're now having some theory around it. But, this is just to was like kind of, can we isolate this and make this work? Right? So, what we did is we took the LLM, we split it into two copies, a teacher and a student. The teacher is the one who's supposed to tell the problems, The student is the one who's supposed to learn a bit on the problems,

**[01:12:43]** and the teacher is rewarded for the improvement of the student. Compared to a student that didn't have a teacher. Right? So, relative improvement. So, this was our idea. It's a simple idea. Was just a bit hard to make it work because you had an outer loop for the teacher and inner loop for the student, and we're not the first one to have these self improvement frameworks. There was lots of work in particular to find some sort of intrinsic student reward.

**[01:13:06]** The teacher would be rewarded for giving a hard question or kind of right question where half of the rollouts would be right of the students, half of them were wrong. So there's lots of intrinsic reward work. And I'll get back to this too. And the other thing is that this was inspired by works, in in in South play, an asset self play. For the last ten years, people have thought about this also in exploring mazes,

**[01:13:30]** and in robotics, and there were these papers by OpenAI in 2021, in particular, that used this kind of idea of a teacher student setup to, improve robotic kind of motion and so on. Right? So, this is not, completely unprecedented. So here's what we did. Right? To come back to this, we have this teacher. The teacher will give question answer pairs. We just ask

**[01:13:52]** the teacher to produce them. They'll be given to a student in batches. The student does a little bit of ROVF on them. And then we evaluate the student on this really, really hard data set that we can't solve, but would like to solve, and see if there's any improvement. And if there is some improvement, the teacher gets a reward. The teacher also does RLBF, so teacher does this also in in groups. And this is the mechanism

**[01:14:13]** we, implemented. Right? So, here is, the notebook LLM version of the same thing. So we did this by level optimization. Which, you know, also has lots of precedent. And, after doing all this, it worked. That's a short message. And it worked. These graphs take my word for it, I'm not gonna explain all these lines, but the blue line is

**[01:14:36]** the baseline, and the top lines, they are not the dotted line, but the other red lines there, is how our various versions of this algorithm actually help and and the x axis is pass at k, for various k in this. Yes. I I I'll I'll So, it worked. It's nice. And it worked even out of domain. So, we trained curriculum, in one setting

**[01:14:57]** for math, and then we had it on Olympiad bench and still the stepping stone curriculum helped. Right? So so this is nice. And I want to also come back to this intrinsic reward As I said, there are several works that already tried this, with having rewards that are not grounded. Not like, how much do you really improve on the real data set that you care about, but more like, is the question hard enough that the student has to think

**[01:15:20]** a bit, but not too much? And, these things tend to work a little bit in the beginning and then a reward hacking hack sets in. I mean, it's fantastic. We run these things It's absolutely amazing what kind of re The the LLM is so creative to hack the rewards. It's unbelievable. So had a lot of fun seeing this, and this is also what people observe. Right? So one lesson here is why don't do the intrinsic rewards not work so well, when

**[01:15:42]** you when you I mean, there's lots here to explore also with more, targeted experiments. Anyway, and one thing, one fun thing we learned was these stepping stone questions that the teacher produced, it actually didn't it didn't matter so much whether they were correct. They were often wrong, as in, like, the answer was wrong. It was like gave, like, what did it give five over nine when it's supposed to be don't know what I mean, you can see here.

**[01:16:04]** So it was more often important to have a correct chain of reasoning rather than have the correct answers. That was fun. We saw that. And now I'm coming to my last thirty five seconds of, view to the future. So, I gave you all this pre history of LLMs, and now we are in this agent self improvement, autonomous AI. And models starting to teach themselves era. And, I think

**[01:16:27]** what's now interesting to understand for our community is basically in these multi agent workflows where we do everything in harness, so you have all these new papers appearing, right, where you don't do RL and wait anymore. You do it RL in harness, in skill. You have to meta learning with writing to the skills, the cloud writing to the skills, etcetera. There's a lot of interesting new questions appearing here. Right? Because we can

**[01:16:50]** also now enforce diversity by having different agents having different prompts and so on and so forth. So there's lots to understand. In these kind of You can also have it We are working on these teacher student setups now for these kind of agentic frameworks. And, you know, we It's it's fantastic. And if there are several agents are better than one agent, all that stuff. But I think the big question that remains here is, whether we can whether LLMs

**[01:17:12]** or models can actually bootstrap themselves out of the best human. Right? So so far, we were in an age where we had data that was annotated by humans. Written by humans, and now it's written, you know, now it's only annotated by the best humans. I mean, if you don't have PhD, don't even work as an annotator. Guess, that's what I hear from on Tropic. Right? Not not Nobel Prize, that's like what they have as

**[01:17:34]** their annotators now. So, clearly, we are reaching level where the best human is passer. Right? I mean, there's very little that the, human can still annotate. I mean, I'm exaggerating a little bit. Another question is, can the model transcend this? And I think you talk to people on the West Coast, they will say, oh, we're already there. I'm a little more skeptical. But we have, we have evidence. Right? Like, look at AlphaGo. All

**[01:17:56]** this self improvement, self, you know, the self play loops, it made it a Go player that is clearly way better than a human. All these games. Right? For code, let's face it. I mean, yes, there are still, hiccups, but it's transcended, but code is very verifiable and constrained. Math, I don't know if you mathematicians, they say never, it will never fall. I think math will fall also, and some point

**[01:18:19]** very soon with these loops, but where's the boundary? Where is there a boundary? Right? What is it about self play that will make it transcend we don't have any more annotation because the human has been left behind? Right? So I think these questions are very interesting to understand. And with this, because I'm already way over time, I'm stopping and you very much. We have time for one question. Further questions can be referred to the

**[01:18:48]** coffee break. So if you have one question, just raise your hand or walk to the mic. Okay. Thanks for the great talk. So, yeah, it's really interesting to to, to to see the contrast between your approach and Jeremy's approach. And so I I I have a question, that that that that comes more from, from from this sort of, like, first principles predictive

**[01:19:16]** science type of thing. Like, I tend to shy away from studying things like reasoning self by curriculum, because I kinda feel like I just don't know how to do good science of this. Because, like, for, you know, for me, I feel like if I can't put the dots on theory lines or something, then I then I just don't know how to trust what I'm doing. So like, how do you think about going about doing this and and and, like, doing science that tells you things that you trust and can build on and all this? Like Yeah. No.

**[01:19:38]** I think it's an excellent question. You, Jamie. Right? I mean, I think of this as first being a sorry. An experimental physicist and then a theoretical physicist in some ways. Right? So I think first, the art is to isolate certain mechanism where you can just have a very simple experiment, like we had with the parity, or, you know, many others, to isolate the phenomenon. I think that's that's number one and that's what makes

**[01:20:01]** reasoning less scary, I think. You just find the thing where it still reasons and you can actually understand the data, etcetera. And then you can sit, I think once you've isolated these mechanisms, and make them smaller, think then you can do the theory, which we did in this by the way, Nikos is here on this first paper, you can ask him question later. But then you can, then you can build a theory, I think. So you have to just first make it less

**[01:20:23]** daunting and then you can attack it. Think. I don't know. That helps, but yeah. Great answer. Let's sing Julia again. And our last speaker for this, first morning session, is David Bao. David is an assistant professor of computer science at Northeastern University. And David David has been a leading figure in, AI interpretability for a long time now, and he's been doing mechanistic

**[01:20:55]** interpretability before the term was coined. And recently, it's been also now applying interpretability to model strain on scientific tasks. And trying to extract scientific knowledge from these models, which find very exciting. He's going to tell us about. And something that you might also not know about David is that he's the author of a very popular

**[01:21:19]** numerical linear algebra. Textbook. Escape and then start again. Yeah. It was showing up. Oh, it was showing? I think it's good. It's like Okay. Very good. Thank you, David. Let's, let's Thank you very much. Warm. I I love I love that progression of talks here and Julia Sock in her last notes that you know, we're clearly in this

**[01:21:53]** this this shifting, this very quickly shifting field in 2026 where, we are now starting to learn how to train these models. To to really see superhuman capabilities I think that it'll be more and more routine. For us to be confronting AI models that we're using in daily life that, seem to know things. That

**[01:22:18]** we don't know. That maybe no human knows, and it leaves us with this question, which is sort of the theme of my talk. Where does that leave us? As people, as scientists and what can we do about it? So what I'm gonna share with you today is a little bit of how to read the science back out of deep learning. I think this is an immature field, but I'll show you a few of the steps that we're trying to take to to do this in

**[01:22:42]** one of the domains. But, but it's a little bit of a shift here for a different topic. So I want to calibrate by asking people who's familiar with this type of experiment? So it's a warm up question. Who who knows what a patching experiment is? What what the what the heck is a patching experiment? It's it's an odd

**[01:23:04]** technique. It's an an empirical experimental technique that's used in my community, but it it isn't that widespread. So, let me just give you this background because it's a tool that is central to a bunch of the methods in the talk. So in a patching experiment, it's so it's it's it's an experiment that you can do with an artificial neural network which is like the neuroscientist's dream. It's

**[01:23:26]** like what if you could give a person like a brain transplant to figure out how their brain works? Right? Obviously, you can't do that with a person. But with a neural network, what you can do is you can run two neural networks either slightly different neural networks or maybe two identical neural networks in slightly different context you know, working on slightly different problems. And then,

**[01:23:49]** you can transplant a neural state from one of the runs to the other run, as a way of asking us as a way of asking, you know, in a very, very focused way What is being represented in that transplanted neural state? Like if you hypothesize that what that neural state has is maybe it's

**[01:24:12]** thinking about the number 14, then you can run the model in a different way where you think maybe it's thinking about the number 10 and you transplant what you think is the encoding of 14 down to the other one and see if you change the behavior of the other model to to behave as if it was thinking about 14. Right? So like in this case, you have some crazy story and

**[01:24:35]** you ask okay, what's what's what's the drink in the cup? And it says tea, and then you have some different story and it's some complicated logic and it says what's It's coffee and then you think, okay, I'll I'll transplant one of the clues down from one run to the other and we'll see does it change? Does it change coffee to something else? And once in a while,

**[01:24:59]** if you bring over the so most of the time, you bring over some state and these experiments fail. Most of the time, your hypothesis is wrong, you try to do a little transplant patching experiment and it doesn't change the output, but once in a while you bring something over and voila, right? You can switch coffee to tea, It gets the model to do something different, And and then you can get very surprising

**[01:25:22]** results when doing this kind of thing. So here's a result from a poster from one of my students. That was presented yesterday. Sorry, this is in the wrong order, so I can't direct you to talk to him at his poster. Because that's in the past, but will be talking more about this again tomorrow at the realign workshop. So in this experiment, you can patch a certain thing and

**[01:25:46]** the original question answers t where you're patching from and you're patching to a run where it said coffee, just like I showed you. But if you patch it different layers, instead of it flipping from coffee to tea, in this particular experiment, if you switch to early layers, it's it patches in

**[01:26:08]** a way that switches the answer from coffee to beer and you can stare at this experiment for a little bit. I'm not going to dwell on it because I don't have time to go through this one today. But I'll talk a little bit more about it tomorrow. But this is this is one of the really puzzling It's like a little Sudoku puzzle. It's like a, you know, it's figuring out like why does it

**[01:26:32]** flip to beer this really interesting exercise in untangling the logic that's that the neural network has learned inside and these patching experiments really allow you to to discover the non trivial algorithms that are learned by by these networks and, and so the structure that I think this community is studying in the abstract,

**[01:26:55]** You guys you know, studying learning theory and how complexity can be learned in in different ways. What we do is we look to see what specific kinds of complex methods are learned and what specific representations are learned in and I think that there's quite a bit of insight that you can get from looking at these specifics. So I encourage you to to see a little bit about what's going on in this

**[01:27:16]** community. This talk today, I'm gonna be talking about work by Kevin Liu to unpack eight AI protein folding models. And so the reason this is interesting is because it's exactly the situation that Julia talked about You know, there's a very expensive

**[01:27:44]** and in the real world. This is you know, this in this example, people are trying to solve breast cancer They know that there's a a a tumor factor that, is implicated in causing breath breast cancer, and they think maybe we can design a drug that stops the cancer from progressing if we can just find some

**[01:28:07]** protein that binds to this and turns off these receptors. Right? And so, the way that you do this today is you heuristically guess many many thousands and thousands of possible drugs and then you have to physically test them to see, you know, do they fold to the right shape? To bind, to the target that you're trying to get? And it costs quite a bit of money every time you do another batch

**[01:28:29]** of these It's another dollar experiment and and the combinatorial space that you have to study is so large. It's really prohibitive to to develop a drug like this. And this is just in the first stage of drug design. So, but what's happened now is the the models like AlphaFold, there's open source ones, there's ESM fold and so on.

**[01:28:53]** That have advanced advanced the the state of the art. They've really revolutionized biology because now you can get such accurate protein folding predictions out of these AI models that you get like a 10 to 100 times speed up. In getting more accurate folding predictions before you actually have to do it in wet lab. And so that's there's

**[01:29:17]** a vast savings and it's really changed Oh, why is this going ahead? Do I have timings on this? I might have to turn this off? Okay. So so, but then it leaves it leaves to this question. You've got this amazing AI, that that you've trained, that can that can solve this classic scientific problem better than any of the

**[01:29:39]** previous algorithms made by scientists. But but it it it leads it leads us to question of what does it leave us humans and scientists Is this science? If we've trained some giant model and it can do the science better than we can, if we don't know how it works? If we don't know what it does, is this you know, is this science or

**[01:30:06]** is this the end of science? And so what I propose is that actually one of the things that's important for us to do is as we start to get AI models that are superhuman that we develop methods for getting the knowledge back out of the models so that we can understand the generalizable principles and maintain our agency, maintain our knowledge, and remain our you know retain

**[01:30:28]** our role as scientists as going forward. So let's let's do this exercise in the protein folding models. I'm gonna give you a little background on how protein folding models work. I think it's interesting. It gives you a little sense for the diversity of different types of architectures out there that you might want to study that are a little different from the language models that are everywhere. So in a protein photo model, the way it

**[01:30:52]** works is you start with a sequence of proteins, so a sequence of aminos. There's 20 different amino acids, When you chain them together, they they lose a couple of atoms and we call them residuals. So you see these letters e v q l, these each one of them. Corresponds to a residual and and then the goal is going to be to go from

**[01:31:13]** the sequence of residuals to a three d shape. And the all the state of the art protein folding models do this in three steps. The first step, is you train it you train it on language model embedding. Just a regular, transformer to take one of these sequences out and then turn it into a vector representation. For for one one vector for

**[01:31:36]** every residual. And then, the second thing that happens is you put it through a folding trunk This is another transformer it's a specialized transformer with an unusual architecture I'll talk about in a minute. That's designed to help folding problems. So it's a little different from a language model. And it's driven by a pair of representations. There's a sequence representation and there's something called a pair wise representation,

**[01:32:00]** which is like a two dimensional. It's a it's a matrix representation instead of a sequence representation. And then after it goes through through 50 or so layers of folding trunk computations, then it goes through a final model called the structure module which which is a readout. It turns all these things into three d shapes. It gives you

**[01:32:22]** three-dimensional locations for every atom. In the in the protein. And, then you get these beautiful three d protein structure predictions out that you can do chemistry with. With. Okay. So, so that's that's the background of what the architecture is. And it and then it leads so now what our question is, is well statistically,

**[01:32:45]** these things are trained to do very well, They do better than all the quantum simulations that people have made in the past. Right? How does it work? What does it do inside? And so we don't have a complete accounting for this. This this work is a preliminary investigation of how the computation is organized. But give you a little sense for how you can make progress with a question like this. So there's three

**[01:33:08]** questions that we basically ask. One is a localization question. There's all these parts of the computation Can we localize where different parts of the computation are happening? Right? Is is the problem just it solved all monolithically or is it solved step by step inside all these layers? And and the typical experiment formed to do this is the patching experiment

**[01:33:31]** that I showed you before. So I'll show you a patching experiment here. And then then then the other questions are, okay, once you see where the problem solved, what concepts are being represented, in this solution and can we directly change those concepts and edit it and verify we've got? Okay. So what Kevin did here to start understanding things is he said, you know, there's a lot

**[01:33:54]** of different problems solved by the protein folding models. But one of the problems is to is to recognize when the proteins fold and it's very narrow a hairpin shape, This very narrow u shape, so that's shown in purple on the right. It's called a beta hairpin. So this is is a place where in the protein it goes out in a flat sheet for several several base,

**[01:34:16]** you know, for several residues and then makes a 180 degree turn and then that folds back on itself. Again. So of like that purple shape. And so, the models are very good at predicting when this happens, and he wanted to understand, you know, how they how they do that. They figure this out? And so, he set up a very simple patching experiment to do this, and let me show you how this works. So,

**[01:34:40]** his intuition or actually it was based on some other experiments, but, you know, his his his found that the main work is done inside this big middle model, the folding trunk. But the folding trunk has two different representations it's dealing with. It's dealing with this sequence representation and this funny pairwise representation. Representation He had no idea where to start Should he

**[01:35:03]** be looking at one of these halves? Or the other half? How can you tell So he set up a pair of patching experiments one on the sequence And what what he does is this. For his patching experiments, he needs to have two runs. He has a run where the it's it's sort of like the coffee and tea setup I I described to you at the beginning. Is one run where

**[01:35:27]** there's a a hairpin being predicted And then, he has a different run, where when the model is acting correctly, there's no hairpin being predicted. It's it's at it's at alpha helix. In the left hand side. It's not it's not a long hairpin. Right? So this protein that this protein sequence he puts in on the bottom doesn't have a hairpin. But his question is, can

**[01:35:50]** he find where the decision is inside the model that causes it to decide to have a hairpin? Can he patch some concept in the middle of the model down to the second run? So that when you run it, it changes its mind and says, oh, you know what? I think that there should be a hairpin here. Right? So that that would that would do it, like that would show him where this localized decision is. And he

**[01:36:13]** and then so I some of this work is quite painstaking. Right? It it took him many months to figure out how to set it up and how to localize this but eventually you got this critical experiment working so he's this is these are his slides. He's so proud of this. Where he he ran this pair of experiments and he found yes, there are two domains where if you patch

**[01:36:38]** a small number of vectors from one run to the other, you can get the hairpin to show up. And, and the way that he does this is he has thousands of proteins without hairpins, he has thousands of proteins with hairpins, and he patches from the proteins that have the hairpins to random proteins that don't have hairpins, and and then he just measures

**[01:37:00]** to see like how often patching it's specific locations has the effect And so the orange results here correspond to the sequence the sequence result being patched. And the green results here correspond to the pairwise representation being patched. And he found that the sequence representation when you patch

**[01:37:23]** it, it very early layers like this first seven layers, of the folding trunk, then you can fool the model into thinking oh, we should have a hairpin. But but if you try to do it with the wise representation at the early layers, it doesn't do anything. You have to patch the pairwise representation way off at layer 30, in order to fool it into having a hairpin. So you can see these very different roles

**[01:37:47]** and and so this leads to his hypothesis that there's two major phases in how the protein folding model is working. There's this early phase where he hypothesized there's biochemical signatures that you get that are local from the the individual residues and then it turns it into a spatial prediction in the second phase. Which you can intercept

**[01:38:10]** in the pairwise representation in the later layers. And so, okay. So now, what are the actual concepts that it's that it's using? What's being passed from this sequential state to the pair wide state. What goes from one to the other? So, what what he did is he said, okay. So let let me let me zoom in to show you what you mean by passing

**[01:38:34]** from one to the other. So inside the folding trunk, you have these two streams of representations the sequence and the pairwise representations. The pairwise representation if you have it's it's an n squared representation. So if you have a 100 residues in your protein then the pairwise representation is a 100 by 100 matrix. Right? So it's it's a 10,000 you know, element. There's like 10,000

**[01:38:57]** tokens. A way of thinking of And and so, so when you enter the folding trunk, this pairwise representation is has has no information about the protein. It's just initialized with, positional embedding. But then, as you go through the layers of the folding trunk, it picks up information from the sequence representation through some

**[01:39:23]** internal data flows in inside. The neural network like this. So there's a pair to a sequence to pair update, where it does an outer product of of the sequence representations to sort of give you an update to the the pairwise representation and and then there's a paired sequence thing that gives you back

**[01:39:45]** the other way. So it's just data mixing technique. And the question is, you know, what's actually being passed? So so what he does is he asks does the you know, do basic biochemical properties do they get represented in one of these sides or the other? So he starts off by asking about

**[01:40:12]** electrostatic charge So there are aminos that have very strong positive charge and different aminos that have very strong negative charge. And he says, can you predict can you read out from the sequence side or the or the pair wise side whether, given amino is positive or

**[01:40:34]** negative. And and the answer is yes. You can. You can read it out basically a 100% but but what the interesting thing is the information shows up in the pairwise side at about layer seven. The information is not there reliably. For the first seven layers, but then but then it's very strongly present in the side after layer seven, which which corresponds

**[01:40:59]** to this transition where the causal experiment said the sequential information is really important up to layer seven. But then after layer seven is not very important anymore, So what this suggests is that layer seven the this biochemical information is passed over to the pair wise side of the representation and and and

**[01:41:24]** and then proceeds on from there. So, okay. So, let me let me give you then there's this sort of the second form of the experiment you do Okay. So let me let me back up and give you the I'm getting a little bit into the details of Kevin's experiments. I'm using his slides here. But let me back up and give you

**[01:41:47]** a sense for what's going on in this type of work. There's basically two forms of experiments you can ask. You can ask is information present And you can ask, is the information actually used by the model? And so in this kind of experiment that Kevin did, it's a probing experiment. It's asking is information present?

**[01:42:12]** Does the model know about charge? And so, he trains a probe to ask about charge and then he uses this probe as a test to different layers of the model, to different components of the model to say, where is information about charge in this model? And he says, oh, it's in the sequence. Part, it's in the pairwise part, at this layer to that layer. The problem with this type of probe is even if the information is

**[01:42:36]** present, the model might not be using it. Right? If the mation information is absent, it's really unlikely the model's using it. Right? If the info even if the information's present, the model might not be using it. So so to to see how the model is actually working, you have to triangulate it And so he follows this with a second experiment, and he does it This one is it's called the

**[01:42:58]** steering experiment. Where he takes a specific vector vector representation of charge, which he gets by taking all the positive residues and all the negative residues and the representation at a particular layer, and just taking the difference the vector difference between the average positive residue and the average negative residue and that gives them a very concrete vector

**[01:43:20]** that just is his hypothesized representation of charge inside the model. And then he asks, can you actually steer the model to behave as if the charge as if it's belief of the charge, was positive or negative by injecting this vector into the model. Like can we can we not only read out the concept of charge from the model, but can we get

**[01:43:43]** the model to think differently by doing it? So, what he does is he takes something that is not not a beta hairpin, and then he injects positive charge into one run, of the, of the model, even if the actual aminos are not positive. He says, he says think that these are positive. He says override the thoughts and then he

**[01:44:07]** injects negative charge into the adjacent run. And what this should do is it should get the model to think it's like a it's like a little fake chemistry experiment It should get the model to think that there's a positive and negative thing adjacent to each other. They should like magnet together. So it's really weird. It's like doing it's like doing chemistry inside the AI

**[01:44:29]** brain. By making it hallucinate that some of the things are positive when they're not and other things are negative when they're not. And and the answer is yes. It absolutely does this. I'll show you let's see if I have a video. So this is is an example of him. Taking something that was charged one way and then he he gives them both positive charge on both sides, and then you can see that he he can

**[01:44:53]** crank open the prediction so that these things are repelling each other and he can do the as well. He can pull these things back together so by making the model believe the charge is different from what it actually is, he can get them he can like do chemistry experiments that are counterfactual in the real world. So that's that's another example. Now, that's that was all sequential stuff. He

**[01:45:16]** also did an interesting set of experiments looking at the pairwise representation And in in this case, he found oh my gosh, slow animations from his slides He what he found was that the pairwise representations actually represent distances like spatial distances between between amino acids. And he can, with a simple linear probe, he

**[01:45:44]** can regress pairwise distances really accurately. Just just in terms of angstroms. And and the interesting thing about that is that he can take these late layer pairwise representations and just physically manipulate the distances to just to just jam things together in different locations. That's that's another way that you can make hairpins.

**[01:46:09]** By taking, the two sides that aren't a hairpin and then reducing the, his hypothesized encoding for the number of angstroms between them he can he can cause them to be a hairpin. I'll show you another video of this. It's kind of interesting. So this is something that's sort of loosely folded. And then he says, oh, actually, want you to hallucinate that these

**[01:46:33]** things should be tighter together, and you can see that yes indeed you know, this this representation of hypothesized risk representation of distance in the model actually is causal for the way the model is thinking. So, and this is this is the stuff that's happening later at layer 30 and so on. So so you can kind of see, okay, this is this is his main findings. That early

**[01:46:55]** on, you've got these chemical properties and later on you have these geometric properties and the model is localizing each one of these properties in low dimensional subspaces at small numbers of tokens and you can you can trace the computation through so that you can actually cause the model to behave as

**[01:47:17]** if counterfactual values are actually held for all these different concepts, these scientific concepts. Okay. So is really the first time somebody's cracked open a protein folding model to try to see what signs of the internal computations are. You can see that know, even after quite a bit of effort, we can only understand

**[01:47:40]** very rudimentary things and it leads you to this question, so what? You know, what's the big deal? So you you know, we have have positive charge and negative charge and we have you know, angstrom differences you know, distances between between atoms. What do we care? That the model is thinking about these things? None of these things particularly surprise. Well,

**[01:48:04]** this is really the way I see it is this is really part of broader research program, a broader research question. Which is you know, if if these models are going to start understanding things better than humans do, then how are we going to with them? They're opaque black box systems. There's really three things that you'd like to be able to do that when the systems

**[01:48:30]** are black box is pretty hard to do. So one is you know, you'd really like to debug, audit, and improve the models. So already looking inside the models, it rate the you know, it raises questions about the architectures Like, if if the early layers are all about the sequence representation and the late layers are all about the pairwise representation then we're do are we doing

**[01:48:52]** a lot of unnecessary computation? You need the sequence representation at layers? Do you need the pairwise representation at early layers? Right? Is this we just you know, sort of throwing in a lot of extra trained? They're sort of dead. Are there ways of debugging, optimizing, and improving the systems, from the insights that we have. I think that's that's that's an obvious

**[01:49:16]** type of thing that the insight that that people will get from this type of work. But then, there's other things that are less obvious, which are interesting. Are there are actually a lot of unsolved problems in protein folding trying to understand how folded proteins interact with each other There are also proteins that change conformation very easily under different conditions,

**[01:49:43]** if you change the pH a little bit, they'll change your conformation and so on. And current, protein folding models they just give you a consensus estimation of what's going on. The interesting thing about understanding how they're computing is that it might give you the ability to control these things in a more precise way. Like just the way that we can change the charge environment to a little bit more positive or negative,

**[01:50:06]** at least naturally leads to the question, can you get the model to do a counterfactual prediction if you change the pH by a little bit? If you dial up the pH can you get the very same model that you trained on a neutral pH training set to tell you what its prediction would have been if And so so I think that there may be practical knobs that we can add to these

**[01:50:30]** models based on the things that we understand in them. That's another research target in the future. But I'd say that the real research target the real long term thing is that these models are doing predictions. That are better than all the previous models that we've made before. They're they're more they're more accurate than you can get out of quantum mechanics. And so the question is, are they doing this

**[01:50:53]** based on principles that we should have in our textbooks? Like new knowledge about how biological mechanics works or new rules of thumb of how protein folding is done. These these unknown rules of thumb are definitely encoded in these models scientists don't know how they're working so well. And so the question is, can you can you roll this

**[01:51:17]** knowledge forward of how they're doing their computations far enough that we can actually write the next chapter of the textbook. And that's really the long term vision and the the challenge that's in front of us. From doing this. And so, that's that's that's my perspective. On this type of thing. I think that a lot of the work that we're very excited by in the field has to do with understanding

**[01:51:39]** language models I think that you have very similar questions that are already being asked about how do you get superhuman capabilities out of a coding language model when you have a language model that's dealing with vast amounts of text. Are there types of reasoning that it can do that actually start to exceed the ability of humans to reason and so, how do they work?

**[01:52:03]** But I think that there's the in a lot of those domains, it's kind of this open question whether the systems are actually smarter than all humans yet, or not, but there are other domains, like the scientific domains, where it's already unambiguous, where the existing AI systems are already outstripping all the previous, science that has been done. And, and so we already are confronted with this

**[01:52:25]** question. Of how how to read the science back out of deep learning systems. Thank you very much. So unfortunately, we're out of time, but this is the break. So if you have questions for David, you can just with him at the break. If you need to the if you need to hang your poster, you can come to us We have the strips and we'll resume at eleven.

**[02:15:36]** Later, so if you have a seat. Can start with the contributor talks. Thanks. Please have a seat. Can we do the poster later, please? So I stocked Okay. So the first contributor to of the day is by Minak Song. Who is an undergraduate student, at

**[02:18:02]** Kaist in Korea. Majoring in mathematical sciences in the group of Charlie Yu, he was also this is a student at Washington. And, he works on bridging Turing a practice in learning theory. And, he has a recent focus on optimization dynamics. So today's going to talk about zero order optimization at the adjustability.

**[02:18:27]** Thank you for your introduction. Yeah. I would like to thank for organizing this work. Wonderful workshop. The first talk of this morning session was from Jeremy about how does screen design work? I would like to expand his talk but and talk about how does zeros order gradient descent work. So this was done with

**[02:18:50]** my wonderful collaborators, Liang, Bingzhong, Yao. Michael, and Sue. So what is zero sorter optimization? It is an optimizer method that optimizes an objective using only function values which means doesn't use gradient. Compared to the first order method. So this is very useful when gradients are inaccessible, noisy, or too costly to obtain. So

**[02:19:14]** in modern deep learning, the most famous method why they use this SPSA, which is used for a zero order grading estimator. And one famous example is called Mezzo, which uses for fine tuning large language models. We just forward passes So it doesn't use any back propagation, so it reduces memory by 12 times. But achieving the similar performance. So

**[02:19:38]** and how does zero third degree in the standard work? So consider minimization problem of optimizing the objective f. And the simplest algorithm, there is sort of gradient set. Updates using this two point gradient estimator. Delta hat f. So it's basically gradient descent, but we replace the with an update with a gradient estimator. And to obtain this two point gradient estimator,

**[02:20:03]** you first sample UT from a standard Gaussian distribution. So this is your perturbation vector. And you perturb x t, the current iterate, through this u t vector. And obtain two point function values, which is f x t plus mu u t and x t minus mu u t, and compute the final difference. And you the two point grader

**[02:20:27]** estimator becomes just this scalar times u t, which is a random vector direction. And here, mu is a perturbation radius. And we can note that if mu goes to zero, then the expectation of this gradient estimator also converts to the exact gradient. And our interest in our this talk is understand the training dynamics of this theory of disorder method.

**[02:20:51]** Operating in deep learning. So let's quickly review how gradient descent works in learning. So in gradient descent, with step size ADA, on a quadratic objective, We see that the iterate would diverge if the step size is larger than two over a maximum value of testing. But, however, in deep learning, just showed that full best gradient

**[02:21:15]** descent operates at the edge of stability, which means that the maximum value of Tessian is saturating at two over sub sites. So to understand the zero sorter grading let's start with a very simple experiment, just training convolutional network on cipher 10. So here we plot Hessian top eigenvalue and also Hessian

**[02:21:39]** trees along green the descent. And also zero order gradient descent. Trajectory. We used three different jet sizes. Each by blue orange, and green colors. So at the top left figure, you see that a typical EOS behavior of Grain is then showing that the maximum iodine value of HSEAN is saturating at two over the step

**[02:22:02]** size. And if you see the figure at the bottom right, the this is the evolution of the Hessian trees along the through sort of gray in the center And you see somewhat a similar phenomena. But a bit different So the trace of HETYAN is now saturating two array minus some delta. So it's saturates slightly below this threshold.

**[02:22:27]** So we can speculate that there is something similar happening for zero to order grid instead. It's something at job stability, something related to the trace of s So the main research questions we want to answer is first, do zeros order method also operate at edge of stability in deep learning? And also, second, if so, which curvature related quantity covering this?

**[02:22:51]** So To answer this question, we'll we'll start with introducing the linearized dynamics So let x star be x star be a local minimizer of f and let h denote the hessian. Metrics at this x star. Then the linear dynamics of this optimizer around this x star is just the dynamics obtained by applying this optimizer to the quadratic Taylor approximation around this

**[02:23:14]** x star. And we will assume that this hessian is positive semidefinite and denote the eigenvalues as lambda one two under the And based on this linearized dynamic definition, we will define a linear stability of the optimizer. So let's let x t be the iterates of the linearized dynamics.

**[02:23:37]** And we will say that the optimizer is linearly stable in the mean if the expectation of x t minus x star is bounded throughout the trajectory for every initialization. And we'll also introduce the notion of mean square linear stability which is defined as if the expectation of the square norm of x t minus x star is bounded throughout the trajectory

**[02:24:00]** every initial iteration. And here, we could easily note that for deterministic optimizer, there's no any stochasticity. These two notions are exactly the same. And we can naturally introduce the notion of critical step size, which is defined as the largest step size that will guarantee linear stability. So the critical step size in the mean we will

**[02:24:25]** denote it as a dot mean star, and we will define the critical step size in the mean square as ADA MS star. So for standard grid and descent, the linear stability is what we know. The critical step size of gradient descent is exactly two of our maximum eigenvalue you have the Hessian. So if the step size is smaller than this, it is linearly stable,

**[02:24:49]** If the step size is larger, then the dynamics would be linearly unstable. So how about the zero third grader grade in descent? So one thing to remark is that since we are considering a quadratic objective, the two point estimator is observed to be unbiased estimator. And therefore, the mean dynamics of the observed gradients tend is essentially same as just

**[02:25:15]** standard graded descent. So the main dynamics are exactly the same, so our main interest would be understanding as mean scare dynamics of theorems that are graded. Descent. And here is the result for zero third degree descent. So it turns out that the critical step size in the mean square is a unique solution of ADA that satisfies these

**[02:25:37]** three equations, which is ADA times lambda max h is smaller than one and the sum of Ada lambda I over two times one minus Ada lambda I is exactly one. So could exactly characterize this mean square step size. Critical step size. And moreover, we could also obtain a lower bound as two over a trace of hessian plus two times maximum egg value of hessian.

**[02:26:00]** And upper bound is critical step size as two over the trace of of Pesion. So we characterized as the critical step size of zero third degree descent, And if we note that if if you know the full spectrum of this Hessian, the exact critical step size can be computed by solving these equations, But obtaining the full spectrum is like unlikely

**[02:26:24]** It's infeasible in practice. So instead we will track upper bound and lower bound, which is only characterized by trace. And the hessian maximum eigenvalue. And these can be efficiently estimated using just hessian vector plot. And we also have results for the momentum and adaptive method. So if you see this table, the first top three methods

**[02:26:50]** are first order methods. We know it's a linear stability condition. And the bottom three is what we have obtained for the first order counterparts. Which is about the critical step size of each method. And one thing interesting here is that if you watch see the effect of the momentum beta, here. For so for first order

**[02:27:14]** gradient start with momentum, if beta increases, then the critical step size also increases. But for for but for zero third degree descent, with momentum, if beta decreases, then the critical step size will decrease by one minus beta. And there's also different effect of beta one in Adam and zero version. So we see that the momentum affects the stability

**[02:27:38]** of first order method and second zero order method in very different ways. So So in experiments, we will track the mean square stability during the training. And we will say zero sort of gradient standards at mean scale edge of stability if two of a data is inside the boundary of trace of HSE and trace of HSE and post two times maximum of

**[02:28:02]** HSEAN and also similarly as zero order gradient semibre momentum and zero order adder. And here is what we got for training CNN on cipher 10. We again track trace of HESEN and also trace of HESEN plus. Two times lambda max of eigenvalue. And you see you see this upward bound and lower bound and the dash line, which

**[02:28:26]** is two arrear. And this dash line is exactly be is exactly between these two values, which means that zero zero zero zero zero zero zero zero is indeed at the minisker edge of several We also did got similar observation, not only for zero sorter grain descent, but also for the of the of the of this time with momentum when varying this

**[02:28:49]** And also for zero order Adam. At right speaker. We also changed architectures to ResNet vision transformer, and all these setup, we observed that they all So And finally, we could also, clearly observe these catapults dynamics, we increase the step size at the middle of the

**[02:29:14]** training. So we increased step size from ADA one to ADA two and ADA two to ADA three. Three. And you see that the trace of HSM decreases as you increase the zap size, and there's a loss spike is a catapod dynamic which is a similar observation we could observe for gradient descent when you increase the step size. So So quick summary.

**[02:29:40]** We obtained the exact step size calculation for understanding the mean scale linear stability for a family of zero order optimizers. And that includes gradient descent. The original version of gradient descent, and its momentum and preconditioned variance. Which is series order atom. And empirically, we observed that the full batch of orders are operating

**[02:30:02]** at the mean scale edge of stable. So the takeaway is that when we use a large step sizes, for zeroth order training, this is implicitly biasing your solution with small preconditioned Hessian traits. Or just small which is different as compared to first order training, which is leading you to small hessian maximum Eigen value.

**[02:30:27]** So here, his entries is much important. For understanding through his order training. And some future works, we could think about central flow for this zero to the gradient stand. And also another future work would be, understanding edge up stability for a series order stochastic gradient descent. Where we use mini batches.

**[02:30:51]** Yeah. That's all. And we also have these archived version of our full papers. If you're interested, you can check out. Thank you. Thank you, Minak. Are there questions? Please, can walk to the mic or I can come with you. If no, let's thank Minak again.

**[02:31:25]** Thank you. So the next contributor talk of the day is by She's a PhD student in the theory of computation group at Columbia University. And she's advised by Daniel Tsue and Alex Andoni. Before that, she majored in mathematics and computer computer science at, UC San Diego. And,

**[02:31:59]** her research is in, machine learning theory and algorithm statistics. And, specifically finding methods to make training more efficient. And, today, she will talk about less data and faster training. Please. Thanks for the introduction. I'm Jing Wen Liu from Columbia University.

**[02:32:24]** Today, I'll be presenting our work on less data faster training. And specifically, how repeating a smaller dataset can actually speed up optimization. This is joint work with Ezra Edelman and Sirbi Goh from University of Pennsylvania. And Bing Bin Liu from Computer Institute and Harvard University. So from the classical point of view for deep learning, more data is

**[02:32:47]** always better. And the scaling law of training LOMs also indicates worse test loss under the data constraint setting. But can less data be favorable in any cases? Prior work has found that under a fixed compute budget, moderate number of repetitions on smaller dataset can actually do much better than training on large data set for some mass reasoning

**[02:33:12]** tasks like common divisor and modular multiplication. We further investigate this phenomenon across several different setups. We We first compare re repeating on smaller dataset with online training in transformers, and using Adam optimizer on four different tasks. Sparse parity,

**[02:33:36]** single image model, in context learning linear regression, and modular addition. And we found out that repeating on smaller datasets with which corresponding to the orange curves, converges much faster than online training which corresponding to the blue curves. So also tried this on MLPs using mini batch gradient descent. And, again, repeating

**[02:34:01]** on smaller dataset learns much faster than using fresh data at each step. And this also holds for full batch gradient descent. Which means each step, we perform gradient descent on the entire dataset In this setting, we compare full batch GED on smaller dataset versus large dataset. So we call this phenomenon the small versus large gap.

**[02:34:28]** And I've shown that the small versus large gap exist across different setups, for example, different tasks, different architecture, and different optimizers. Which indicates that repeating smaller data set can actually be a favorable inductive bias for optimization. And we aim to understand why this happens. I'll first explain why the existing theory cannot

**[02:34:53]** explain this, and then present our hypothesis formalized by theory and supporting empirical evidence. For this talk, we just gonna focus on the parity task. Formally, a decay parity takes input drawn uniformly from a d dimensional hypercube. There's, hidden support set hidden support s of size k. And

**[02:35:19]** the label is the parity on the coordinates in the support s. So Okay. There are some prior work that showed that repetition can make SGD algorithm go beyond CXQ algorithm. And have the power of SQL algorithm, which is a much more powerful class But for a parity, there's no distinction between the C SQ and the SQL lower bond.

**[02:35:46]** And another explanation could be repeating on smaller dataset can reduce the gradient variance. But this doesn't apply to the full batch GED case. Where there's no gradient variance involved. And some other work also also show that if the input distribution is biased, there are some low lower order signal that can be exploited. But the signal

**[02:36:10]** decays exponentially in k, which can be very weak k is large. But we still observe the small versus large gap in the dense parity setting. So our hypothesis is that the sampling bias from the smaller dataset can help adjust the relative norm across layers a desirable way. To be more clear, the sampling bias of a dataset of size n is roughly on

**[02:36:36]** the order of one over square root of n. And repeating on a small dataset keeps reinforcing this bias which leads to the rapid growth of some layers. Let me illustrate the intuition on the two layer MLP setting. The sampling bias can grow the norm of the second layer which is the parameter a, very fast, and which in turn speed up the feature learning in the

**[02:37:01]** first layer for w. Because the gradient of w depends on the gradient, depends on the normal a. And we also empirically observed this Here, we can see that in the smaller data the smaller data set grows the ratio norm ratio between a and w. Much faster than larger dataset. At the initial phase of training.

**[02:37:27]** We further formalized this, intuition, you know, two layer quadratic activation model with correlation loss. We analyze a two phase training strategy where we first train on random subset of the population with size n, and then switch to training on the full population. And the simulation also aligns with our intuition that the first phase

**[02:37:49]** smaller data set grows the a faster, and this induced faster feature learning in the second phase. And we can prove that in this setting, the number of steps needed for convergence is smaller when the data set size n is smaller. Okay. So far, I've I've been showing you the theoretical intuition for the hypothesis. Next, I will present some empirical evidence

**[02:38:13]** our hypothesis. Since the role of sampling bias is to grow the second layer, The any approach that grows the norm of the second layer fast should also give similar speed up. And the signal doesn't have to be relevant to the target function. Therefore, we test our hypothesis by first repeating on a smaller dataset with random labels.

**[02:38:37]** And then switching to the large dataset. Here in the, figure, the green curve is training with a random label. And we can see that it is comparable to the orange curve is repeating on a smart data set with true true label. And on the right, the growth rate of the norm ratio between first layer and second layer only depends on the size of the

**[02:39:00]** smaller dataset. We can also directly initialize the second layer norm. To to be larger than first layer. And in this figure, the x axis is the unit scale for the first layer, and the y axis is the scale unit scale for second layer. And the lighter color means the better accuracy. The red star denotes the sender initialization scale.

**[02:39:26]** And, indeed, we see that large set training is much faster when the scale of the second layer is larger and the first layer scale is smaller. So in this case, we can see that at the best layer wise, initialization scale the small versus large gap can be closed. But repeating on smaller data set is much more robust on different initial initialization scale.

**[02:39:54]** We can also, instead of growing the norm of the second layer, we can also just directly use layer wise learning rate. This can also close a small versus large gap. Here, the dash lines are using the optimal layer wise learning rate. Which is which uses a much larger learning rate for the second layer than the first layer. So We further confirm our intuition

**[02:40:20]** on the transformer model where we focus on only the QK matrices. Because it directly affects the attention part of the transformer, And we found that increasing the learning rate for the QK or increasing the initialization scale for QK And adding QK normalization can also reduce the small versus large gap. So Finally, I want to discuss,

**[02:40:46]** some setting which can make the small versus large gap larger. First, we observe that the gap grows significantly larger as the model gets deeper. Or the model width gets smaller. And or the or the task is being more complex. Okay. To summarize, we found that repeating on smaller dataset can be a favorable

**[02:41:19]** inductive bias in optimization. It it it can give speed up comparable to exhaustively tuning tuning learning layer wise learning rate. Or layer wise initialization scale. The latter can be very computationally expensive. To tune when the model gets deeper and deeper. And we'd identified that the speed up is mainly due to the larger

**[02:41:42]** sampling bias from the slower data set. Which gives favorable relative norm growth between layers. I Okay. You might wonder, when does the small versus large gap exist? We believe that the loss landscape needs to be nonconverged and have many saddle points. And we confirm that it doesn't exist in the linear regression setting.

**[02:42:08]** Connecting to practice we don't think the small versus large gap exists in when the training data is already very redundant. And this is the case in LMPT training on on large web dataset. However, believe that this exists when the when we're training on more structured data. Such as formal reasoning tasks,

**[02:42:32]** And this has been confirmed by a concurrent work, which also demonstrates a small small versus large gap in RNN post training for mass encoding datasets. Okay. I will conclude my talk from here. Thanks for listening, and happy to take any questions. Thanks to the speaker. Are there questions? Thank you for great talk. So,

**[02:43:09]** based on your theory, is it possible to suggest how many samples we should use or mean, any idea? So before starting training, it's it possible? Oh, yeah. I think the the it's pretty robust across the, hyperparameters. So just make sure the the smaller dataset is small enough

**[02:43:35]** so that, training, the training loss can quite quickly overfit to the small dataset. And then later use a large data set to ensure generalization and this will generally give speed up. Sorry. But the too small, it it overfits. Right? So So that it it can quickly overfits to the training data. And that the best number of samples can

**[02:44:00]** can we see beforehand? Sorry. What what what do you mean by that? We don't like overfitting. Right? Oh, oh, slightly overfitting is okay. And Slightly. Yes. Yeah. Slightly. But but, I mean, just one sample is Oh, yeah. Like, yeah. It Yeah. It it has to learn some meaningful, stuff from the task. Yes. And my question is about maybe lower bound of

**[02:44:24]** number of samples you need we don't have a rigorous lower bound, but, I think, first, like, your model needs to significantly from the insertion. And that's that's the general strategy. Okay. Thank you. Yeah. Other questions? If not, let's thank Jing Wen. Thank you.

**[02:44:58]** Next speaker, is, Bruno Lorero. He's a CENRS researcher at the Ecole Normale in Paris in the center for data science. He's a prominent figure in statistical physics using, methods that come from, disorder systems theory. To crack problems in, machine learning. Theory. And today, he's going to talk about optimal

**[02:45:21]** scaling loads in learning year after multi index models. And, Bruno. Florin. Thank you for the nice introduction, Antonio. So, yeah. Today I'm gonna be presenting you this work with my PhD student Leonardo De Felipe, and my great collaborators Anton Meyer. And Fillon Jacalab. So before starting to the paper, I would like to share with you, like, this which

**[02:45:43]** is an extract of a paper written by Liu Brimon think is very much in the spirit of this workshop where he's advocating that our fields would be better off with fewer terms, less emphasis on FADG stuff, and much more scientific inquiry in engineering but the latter requires real thinking. So actually the reason why I put this slide is because, you know, as a physicist thinking about theory of machine learning,

**[02:46:06]** essentially, I'm both like a believer and a preacher of this philosophy, and, of the workshop philosophy. But this paper that I'm gonna be presenting to you today, probably one of the most kind of mathematical and TCS like paper that I that I have. So, yeah, that's an apology, and I tried to make it as scientific as possible. For this workshop. So let's get

**[02:46:28]** going. So what is the key scientific idea in this paper? Is this notion that feature learning can be understood as a spectral transition in the weights of neural network. So here, I'm showing you some empirical evidence from different, papers by some colleagues, who have been looking at that empirically. Have been showing that throughout the training, as you train your neural network, the spectrum of your weights

**[02:46:52]** going from being like the spectrum of a random matrix that's in because you start at initialization, with random weights, and then as you train, you get, like, spikes that get out of the bulk, and these are associated with feature learning. Now, these are empirical observations and some of my work over the past few years have been trying to understand this like, in simple models much much in, like, in the same philosophy as,

**[02:47:15]** Jeremy was advocating the first talk. So, we have studied a lot, like, feature learning in what is called like multi index models, which are kind of models that translate this inductive bias that data leaves in a low dimensional sub and so you know, learning features mean to learn these directions, which are hidden. And so we had a lot of papers about that, where you

**[02:47:37]** can make very concrete this idea that, you know, at initialization, or when you have very little data, you're truly in your network weights are essentially random, so you cannot capture anything about the information on the data, and as you do grading descent or as you add more data, you start correlating with these hidden directions in this multinox model. So, you get, like, this kind of spectra transition with a spike

**[02:48:01]** out of the bulk, and this spike is correlating with this directions w one, w, r. And so, as you keep increasing or you keep training more, like, you get more and more spikes, and then you can see like as the networks get better and better in generalization, essentially what you're having is like more and more spikes. So, this has been, worked in the different papers, that I'm I'm citing here.

**[02:48:22]** So, the goal of this paper, specifically, is trying to make sense of, new scaling laws using this framework. So, for those of you who don't know nearest scaling laws, this has been an empirical observation that had major impact in practice over the past few years. And essentially challenges this traditional point of view that more is better. Right? Like, I keep increasing my network, gonna get

**[02:48:47]** better and better. So, that turns out not to be true, unless you actually scale different quantities together. So, both the number of parameters, the quantity of data, and the amount of compute that you spend. And actually, empirically, you can describe this relationship as a power law into these three parameters. So, this is an empirical observation in large language models. And from

**[02:49:09]** the theoretical perspective, we do have some understanding of this phenomena of scaling laws, but mostly on linear methods or lazy training. And I guess, have some people in the audience that have worked on that as well. I have worked on that. And actually, this kind of saturation phenomena that you get if you just scale one of these parameters without keeping, like, keeping the other fixed, can actually be understood in these

**[02:49:33]** kernel methods, and so here, just showing two plots from my own work. Or have studied that. But, as I said, many colleagues have worked on that, and guess that we pretty much understand this saturation phenomena in linear models. So, lately, I have been thinking a lot on how can we make sense of, putting together feature learning and scaling? And in particular, how

**[02:49:56]** scaling improves as you train and as you learn features. Because in all these cases, essentially, the weights of the neural network are random or fixed. So you don't have, like, this adaptivity, which is so important when you actually deal with real neural networks. So, the starting point, on this journey has been this paper that actually we presented as an oral here, at a clear

**[02:50:18]** last Friday. In which we studied this problem in the context of quadratic neural networks. And, again, I'm gonna resonate on what Jeremy said, like, you know, we should start by whatever is simpler, and more complicated than a linear model is a quadratic model. So, this defines a class of tasks, which you can see as like a composition

**[02:50:40]** of several quadratic polynomials, and this composition is hierarchical. Meaning that, you know, lower order terms in this composition are less are more important, and then as you go up in the sum, the different directions that, that are in this multi index model, they are less and less important. And you can think learning in this problem as, hierarchically, learning these different tasks.

**[02:51:03]** And the power law comes from the fact that as you aggregate the tasks, you know, you have this, like, decaying importance. So, in this paper that we presented on Friday, essentially, we have a theory to describe learning, of this model with a quadratic network. So, this is a quadratic task can be learned with a quadratic network, and essentially, we have a whole phenomenology of how different

**[02:51:26]** scalings on this problem appear in terms of different spectral transitions on the weights. And a crossover between different scalings, just like as is observed in the neuro, scaling laws in LLMs, can be described in this simple model, in terms of crossovers between different rates, which are associated to different spectral regimes into the neural network. So, the question we

**[02:51:49]** posed into this paper that I'm discussing here today is, yeah. Quadratic is nice, but, you know, we would like to say something about two linear networks in general. So can we go beyond quadratics? And so the natural candidate for that would be instead of having, like, a sum of quadratic tasks, now we have a hierarchical sum of of different tasks with like, you know, activations, which

**[02:52:13]** is are more general than quadratics. And the main idea is to use this is a kind of spectral transition picture to see if we can say something about that. Now, this is a slightly harder problem than for quadratic neural networks, but some things can be said. So, the first result in this paper is essentially saying that the rates

**[02:52:35]** of the quadratic network learning this hierarchical composition of quadratic tasks, is universal, in the sense that for any activation that has, what we call, like, an information exponent too, so you can think about, like, just even activations. The rates that the neural network achieve are the optimal rates. So here, is described by these two rates here

**[02:52:59]** in these two different regimes. So the way we prove this in this paper is, you know, in a very good, TCS fashion. It's like to do a upper and lower bound of the of the of the risk, So let me give you some intuition. So the upper bound is basically building on a line of work on spectral methods, so we we propose a spectral method, analyze that

**[02:53:22]** the you know, the top eigenvectors of this spectral method correlate with the directions at the rate that is given here. So, at least, we have this upper bound saying that, you know, if you have this spectrum method, that the the optimal rate can only be smaller than that. So, these build on lines of work, that I'm putting here below, also by people in the audience.

**[02:53:45]** So, the lower bound instead we consider, an oracle that says, you know, imagine that you have learned all directions except one. And now the complexity of learning in this direction goes back to a single index model, and it turns out that we understand very well, how like, the optimal error goes for learning single index models in terms

**[02:54:08]** what is what is called, like, the free energy potential, And, this gives us, a lower bound. So this is like, the first result saying that, you know, we have more general activation, we can achieve the optimal rates efficiently with this you know, two two, algorithms. Now, the second main result in the paper it's,

**[02:54:33]** what happens when you get, like, actually truly in your network? Because a truly a neural network, you know, is not implementing this spectral method, or this oracle. So, what we can show here, is not as strong as what we can show for the quadratic network, but we do we can show that if you consider a is still is a lies version of gradient descent, where first, you do a spectral

**[02:54:55]** initialization on the first layer weights, and then you train the second layer weights by doing ridge regression. You can prove that the rates that I showed you before, so the optimal rates, actually can be achieved by the two layer neural network. And so, this this uses, again, like builds up on, some recent progress, both on spectral methods, and on considering

**[02:55:17]** ridge regression with correlated features. So this is just showing you, like, a little plot that, that show you, like, optimal rates and the crossover. Between the two optimal rates. When you're learning different target functions, which have this information exponent true, with this with this, this stabilized version of gradient descent, where you separate, like,

**[02:55:41]** you know, first subspace recovery, and then feeding the second layer. Like the nonparametric part. Okay. So this is essentially what we do in the paper, let me conclude. So, what do we did I show you today? I showed you that, feature learning can be understood as spectral transitions on the weights of the neural networks. I showed you that, the hierarchical

**[02:56:04]** multinix models are natural models for studying scaling laws in this feature learning regime, And, finally, I showed you that, you know, two layer neural networks trained in this stabilized version of, gradient descent can achieve these optimal rates efficiently. So, if you want to know more about the technical details, which I didn't cover here, I have a poster here. So, you know, this I think

**[02:56:26]** is the last talk of the contributor talk. So, you know, if you want, can go come and check chat with me. So that's the paper. Again, thank you for my collaborators, and if you have questions, I'm happy to take it. Thank you, Bruno, for the talk. Other questions? Do you expect, similar phenomena if instead of a sum or single index model, I have a

**[02:57:01]** multi index model, but somehow each additional coordinate influences less and less the output. Like, is there something special about the separability here or No. That's that's a good question. Actually, there is nothing special. Actually, in the paper, we we we can deal with the case that you are just a bit tricky to define what means like, less and less important, an environment way, but, but we we can we can handle this case as well.

**[02:57:24]** So the separability is not important. The the hierarchical structure that different directions require, let's say, different directions are more important than the others, and they the gap between them of know, follows this kind of powerless structure. Is what is important. Other questions? Okay. Saks, bring on over a talk. I have a question about your last

**[02:58:02]** part, So if we use a special initialization, so what is the time in of this phase? So it will be the log d. Time or it will something like this? Yeah. Indeed. If you if you if you're doing, like, you know, power iteration, that would be a log d. Yeah. Yeah. So, okay. This is my following question. So I

**[02:58:23]** find that not just in sync on text model or marketing app model, Also, in other settings, I find a very in switch interesting theoretical performance is. When we have the two stages two free transitions, normally, in the first phase, normally, we'll take the log d or log d some step. And then in the second phase, you

**[02:58:45]** it will normally enter in a lazy or the linear regimes. We'll take the form of exponential. And learning rate or something like convergence rates. So I'm wondering, do you have some thoughts about this? So I I I don't think you can get rid of the log d. So at least for this class where you have, like, information exponent two functions, you always have like this saddle initialization. So I think you cannot get rid of these, like,

**[02:59:08]** log d factor in time. Yeah. Yeah. So in real life, the hierarchical structure has a linear part. Probably, like, you get rid of the linear part first, and then you get into this trouble. Having to to deal with the log d of the quadratic part, but I don't think you can get rid of that. Yeah. Yeah. Yeah. Okay. Thanks. Other questions?

**[02:59:36]** If not, let's thank Bruno. Thank you. And now we have the poster session. To have more discussions. If you wanna continue Hello. Hello. We're gonna resume, with our next talk So if you would please mosey over to your seats, turn your eyes away from the

**[04:45:34]** extremely well composed and attention grabbing posters. And we'll have a talk in a few minutes. Thank you. Alright. Let's start. So our next speaker is professor Rich Bronick. He's a professor of, electrical engineering computer science and statistics at

**[04:46:11]** Rice University He has made major contributions to and classical signal processing, like multi scale image models, compressive sensing, and many more. And more recently, he has been an advocate at free and open source education. And today, he's going to tell us about what happens when generative models

**[04:46:37]** consume their own output. Very fun. And creative research. Thanks. How's that going? Working? Okay. It's great. Hello everybody. Great to be here. And to talk a little bit about the science of self consumption in AI. And I'd like to dedicate this talk to Tan. Who this

**[04:47:16]** morning was given the award coming from the furthest away to ICLR. So let's give Tann a round of applause. Okay. This is joint work with some, some of my students and, collaborators. So thanks. In, and MTI's and Atlas. So I have a quick question. Does anybody here have

**[04:47:40]** enough data? Nobody has enough data. You have enough nobody has enough data. I mean we're running out of data. We're either running out of data or we have run out of data. And this is means that we're gonna be in a situation where performance is gonna be harder and harder to improve. In let's talk in just as talk about, in generative modeling.

**[04:48:04]** Okay? Now, some of you will say, wait a minute, we're not running out of of data. The world is full of data. We're generating huge amounts of data every day, using a whole variety of different generative models. And so a very simple thing to realize, wait a minute, Why don't we train our next generation generative AI models Why don't we train them on synthetic

**[04:48:27]** data? Right? Like, why not? Everybody's doing it. Right? Everybody's doing it, so why why shouldn't we? Right? Now some of you in the room will be a bit kind of reticent to bit bit kind of conservative, and you'll say, okay, No. I wanna be super clean. And I'm only going to train on verified real data sets that have been created by

**[04:48:50]** careful curators. Right? Data sets like Leon b, or Leon five b. Which happens to be polluted with a huge amount of synthetically generated images. Right? And so it's just inevitable, unfortunately, that we're just moving into a world where we're gonna be learning new models, by you know, using the real data that's out there, but also

**[04:49:14]** by consuming data that's produced by similar or previous generation synthetic Gen AI model? And so this talk, I just want to address two sides of this the science of of this issue, the first is you know, what can go wrong when this when we do this? And then the second is is there anything that we can actually

**[04:49:36]** do about it? Okay? So part one, let's talk about very simply this this idea that you could think you could call self training. So what is self training? Self training is the purest idea of using Gen AI to train or improve Gen AI. So you start on the left, with a hopefully very nicely curated

**[04:49:58]** real right, real data set, You learn a model, and then, you fine tune that model or improve and using out the outputs in this purest of situations from that very same model. Right? This is called self training. You can see it's creating a some kind of self consuming feedback loop. You can do this over many generations,

**[04:50:22]** and you would hope that as you continue to train with more and more of this synthetic data, your performance will increase. And unfortunately, what happens is it it doesn't increase. Okay? It actually creates models that go that go mad. Right? That go that go kind of crazy what happens is performance actually deteriorates. Rather than improves. And by deteriorates,

**[04:50:46]** I mean both in terms of let's say metrics like FID goes up instead it goes down. And also an increasing number of a these striations on on the imagery that's generated. K? So this is one example of using a model to trying to fine tune it on itself and and and going into some kind of madness.

**[04:51:11]** If if you push it even further and say, well, now I'm going to use models that are biased towards producing high quality output. There's two ways to do this. First, very many general AI models out there ship with the knobs tuned towards generating more, like, high quality images, which are closer

**[04:51:34]** to the modes right, of the distribution. Also, people will generate imagery, Right? Imagery using these models. And they're not gonna they don't put the bad examples up on the web. Right? They repost the good examples, and they cherry pick. And this is another kind of bias. And bias models actually run into a special kind of madness, that you've probably heard

**[04:51:58]** of, and it's called collapse. Here's an example taking StyleGAN two model, the is a classic generative model, and again, fine tuning it based on itself generation one, generation two, three, four, and five. And you see that basically the distribution of this model, the kind of images it can create, are basically collapsing to this one

**[04:52:22]** to this one, person. Right? So there's been some initial science analyzing these situations. Some work, out of my group some work from the Shumilov brothers. Julia's group. Where's Julia? She's here somewhere. Starting to study some of the, implications of of this self training. And and we do

**[04:52:48]** know some things. Right? We don't know everything, but we know some things. First, we know that this this this idea of training on synthetic data basically leads to a distribute leads to the distribution, the synthetic distribution taking a random walk. Right? So it just walks around space, what our distribution space. And what that means is that basically any performance

**[04:53:10]** metric that you might pick is gonna deteriorate because the the true distribute the the true distribution and the synthesized distributions are gonna become further and farther apart as you do this random walk. Moreover, if you have biased sampling, like we talked about, the variance of that distribute, synthesized distribution is actually going to collapse. Down to zero. Right?

**[04:53:33]** Thinking in terms of metrics, machine learning metrics, like precision and recall. Either precision or recall or both are gonna decrease And AMP artifacts like we saw earlier are going to going to increase. K? There's a lot of since we're talking about science, there are a lot of analogies with these kind of positive feedback loops. One is in biology. The is

**[04:53:55]** basically inbreeding. Right? We're creating a kind of Habsburg AI. Okay? And another very apt analogy is is to mad cow disease. Right? Which basically where it's kind of extremely apt because it was basically from animals that were fed brains of dead animals. Right? And we're what we're doing is feeding AI

**[04:54:19]** brains right, on previous generation AI brains. Okay. Another, analogy is from mathematics and control theory. This is basically, you can think of using ideas like positive feedback loops from control, Martingale theory, contraction mapping. A lot of these ideas have have been useful in trying to analyze what what happens, when we train models.

**[04:54:44]** On their own But there's still, like, a ton of open questions in this space, and let's just go through them really quick. The first is, everything that I've talked about up to now, at least the examples that I showed, are pretty idealized. Right? You're taking a some diffusion model, and you're training it on the output of that very same diffusion model. Right? This allows you

**[04:55:08]** to prove really nice theorems, but course, this is not what's actually gonna happen in practice. So what we need to do is think about more realistic training scenarios. What happens when you train a diffusion model on the output from say, a StyleGAN? Right? Or some brand new model with the output of some state of the art, let's say, autoregressive type model.

**[04:55:31]** So the fact that the big hyperscaler companies are are trying to do things like data filtering, data verification. Folks talk about watermarking in imagery, even though it's very easy to easy to turn off, and most users actually do turn it off. But this this this key idea, I think, of of trying

**[04:55:53]** to make things more realistic The second is if you just read the popular press, there's a tremendous amount of buzz out there about the fact that that AI slop is starting to pollute that not only the the Internet, but also the the training pools future AI models And I think a really interesting problem is actually looking at going out, looking at

**[04:56:17]** data today versus data, say, five years ago, eight years ago, and actually seeing if we can detect that some of these positive feedback loops are starting to to activate. I think that'd be a really interesting really interesting problem. Very related, is the idea that as these models as like AI type models might collapse,

**[04:56:40]** or might drift away from reality, Who are the consumers of these models? Well, humans consume the outputs of these models. How is that going to affect our brains? Right? That There's this very interesting psychological question about about how this AI collapse could actually cause some amount of, like, human brain. Collapse. And then finally, the thing that

**[04:57:02]** I'd like to talk about for the rest of the talk is around basically, is this a dead end? Like, are we doomed? Right? Or is generative AI doomed because of this? Or actually, is it possible for us to build either, generative AI methods that are resilient to synthetic data, Right? Or, like, that's at the very least And at the very best, we somehow use

**[04:57:27]** we somehow do that, turn this this what seems like a problem into an opportunity? K? So that's what I'd like to talk about for the next next few minutes. That is addressing this open question, right, which is can we actually use the output of synthetic AI generators to actually truly improve the performance of synthetic AI generators. And

**[04:57:51]** it turns out that you can. Right? But the critical thing is that you need to treat the real data the You can't just lump them together If you lump them together, we are doomed. But if you treat them, consider them separately, it's actually possible to improve models, and that's what I'd like to talk about. The key the key realization is that this progression, going

**[04:58:17]** back to the very first is of collapse or going mad, this performance degradation, right, from left to right, right, as we go from a model trained on real data to a model that's been trained successively on synthetic data, it turns out that there are signals embedded embedded in this progression that are extremely

**[04:58:41]** informative, Right? They're informative about the the degradations and biases in the generative model. It's and and this signal can actually be used to ameliorate those biases and those degradations. And I'd like to talk about just one example of how you how you can do that. Okay? So here's a here's an example

**[04:59:04]** of of of kind of the the the basic setup here. Let's say that we wanna learn some, you know, generative model, and we've trained it on, let's say ImageNet, Okay? So we've trained our in our generative model on ImageNet. And the ideal set of parameters right, if we had infinite data, is like over, let's say over there,

**[04:59:28]** in that corner of the room. So that's theta star is way in the corner of the room. That's the best possible parameter. We've trained our model on ImageNet, So we don't have those parameters. We have the parameters that are right here in the middle of my chest. Okay? These are the parameters They're pretty good. Right? But we'd like to be better. So how can we improve our model? There's two

**[04:59:50]** ways that you can think of it. Doing it. The first is you could go out and actually acquire more real data. Right? You could do that. You go you've trained on ImageNet, you go you know, poll the world and and get a whole bunch more like, real real another million ideal, real images. And then what it it turns out is that if

**[05:00:12]** you now fine tune on those real images, and compute the gradient, from this point that would improve the set of parameters, it should be clear if you have more real data, the gradient is going to point towards the corner of the room. Everybody see that? Nodd of the head. Okay. But of course, we we we can't go get more data. We're stuck. Right? We just have we're stuck with the model

**[05:00:33]** that we have. So the the alternative is to say, well, let's generate a whole bunch of images from my model, and then let's fine tune on those images. Okay? Well, of course, we're not gonna the gradient with to the towards a better model. It's going to take us towards madness. It's going to take us out this way. Okay? And so this is where you would you might think, okay,

**[05:00:57]** I'm doomed. There's nothing I can do because if I fine tune on this on on the synthetic data, I'm just gonna move away from my ideal parameter. K? But if we it it just turns out, and it it it sort of was extreme surprise to us, It turns out that this direction is this bad direction is basically the negative

**[05:01:21]** of this good direction. Okay. It seems crazy, but it's true. Okay. So if you define what we call the alignment, which is just the cosine similarity between this gradient direction, the bad one, and the good one, Okay. What we what we can actually show if you go to the very bottom of the slide, is actually the inner product between these is negative. Which

**[05:01:43]** means if you right, which means that if you flip the bad direction, it's actually going to point more or less towards that corner of the room. Okay? And this is something that we've established you know, theoretic, like rigorously. For a a a really important case of of generative models that are called mode seeking sampler. K? And it turns out that, like, most

**[05:02:08]** of the certainly image generators out there, that are used both in the literature and that are used are what are called mode seeking samplers. And the key idea of a mode seeking sampler is it introduces a bias when it samples from its learned distribution. Okay? So the the the generative model has learned this blue this nice blue distribution. But when it actually generates

**[05:02:32]** images from that blue distribution, It's actually set up to generate them closer to the modes Right? And, than out in the tails. And so what tends to happen is with these mode seeking samples, you tend to get mode amplification and tail attenuation. And we can actually take that into account to show these directions are actually the

**[05:02:54]** negative. Of each other. Okay? Hopefully, this makes sense. We call this idea neon, and we call this idea of taking this bad direction and flipping it around. We call it negative extrapolation. Because we're not extrapolating away extrapolating in this negative direction. So here's the basic idea of how this works. It is just extraordinarily

**[05:03:17]** simple. So let's go back to our setup. We have our model. We've trained it on real data. Okay? We actually don't even need to know the real data that it was trained on. K? We have our parameters. Of of the of the model, theta r. And then what we do is we generate a few just a few more synthetic images directly from that generative model.

**[05:03:40]** Okay? And then we take a we take compute the gradient. Right? Well, and then we just basically optimize fine tune with those images. You don't need gradient. We just fine tune with those images to create a new model Right? Same architecture, new parameters, with parameters theta s. Okay? And then what we do is rather than use the model with parameters

**[05:04:03]** theta r, the original model, or the parameters with theta s, the new parameters, we combine them. Basically merge them such that we're basically, essentially doing Theta r minus theta s. With a sum like step. Step size w. K? So it's an extraordinarily simple algorithm and it's basically just a a parameter. Merging.

**[05:04:26]** Super simple, but it works like super well. K. So here's an example of taking the x a r l model which is a high performing high performing image generative model. Okay? Some, four examples of images from synthesized from that model in the top. I'd actually never seen a car like that in the upper left until I got here to Rio. And realized that there actually is a car that looks

**[05:04:49]** like that. So what we did is we took that model, and then what we did was we just compute it was trained on ImageNet, lots of images. We generated just a thousand more images. Tiny number of images. Fine tuned on just those thousand images, k. It turns out it was like about 3.3% additional compute And then we combined, right, Theta r and Theta s

**[05:05:14]** in this neon way, and kind of magically, the FID drops about 25%. Right? So just crazy how well you can improve a model by exploiting the fact that you know there's a degradation happening Right? And you can account for it by by just a few few samples. Okay? So so the thing I wanna you

**[05:05:36]** know, get across here is that this idea is like super practical. It's just a simple parameter merge You don't need anything extra. There's no extra model. There's no inference. Change. There's barely any additional computation. You don't need access to the original data. It could be know, a pre trained model. It works for any mode

**[05:05:59]** seeking sampler, which is, like I said, almost every almost every image generator and tons of text generators, as well. And it's extremely efficient and based on actual theory. Right? So Euro loves it. He said that it, it lights it lights his fire. Okay. So just couple quick example, you know,

**[05:06:21]** to some some, like, showing you that, you know, the trade offs and and, you know, how performance improves From left to right, we are we have the F FID We have the, actually here we're just looking at FID. As we as we basically vary the number of synthetic images right, that we're using to fine tune on when we're varying this

**[05:06:45]** w parameter, which controls how much we merge in this bad direction. But the the point is you can see that all of these curves have basic the same shape, and this is across diffusion, and flow matching models. Autoregressive models, inductive moment matching models, all basically the same. That there's a w right, that you can find with a simple grid search, that's,

**[05:07:07]** you know, substantially improves on the FID using just a very small number of additional synthetic images. Okay? There's if, you know, you can't get something for nothing, there's a no free lunch result. And that is you can't improve both precision and recall using this method. Turns out that

**[05:07:32]** what this neon in particular does is it tends to squash down the mode pull up the tails a little bit of the distribution. So that causes recall to rise, precision to fall, but recall basically rises more than precision falls, and so the net effect is that the FID actually improves. So there could be situations where you're,

**[05:07:55]** know, you you can't sacrifice any recall, but if you're I mean, precision, but if you're you're willing to this this method is gonna improve FID substantially. And I just will mention, there's not really any time to talk about it today, but if you're a fan of class free guidance like CFG, you can combine it and neon to basically

**[05:08:17]** have it kinda have it both ways. So the precision falls very, very slightly. But recall rises substantially. But that's something I can talk about with folks after. K. We have been exploring some variants of this idea, in fact, neon was based on an earlier method that we have called SIMS, and SIEMs is basically the same idea.

**[05:08:42]** This idea of degradation direction, and then merging right, the degraded and the pre trained models together. But it does it not in parameter space, but in score functions space. So it it's merging, like, in the in the distributions. It turns out, this method also works really quite well. It it it designed for working

**[05:09:05]** just with diffusion models, so it's not as general as as Neon. It's also a little bit more expensive. Neon is basically free. But with with, Sims, you actually have to have to actually change the inference algorithm, so it's about two times two times more expensive. But the really interesting thing, like scientifically, about SIMs, is it turns

**[05:09:28]** out that it works continues to work really well even if the original data the the supposed real data, that you used to train your model on originally, was polluted with synthetic synthetic data. Okay? And this is really quite a strong effect. We see that, you know, you can have up to like 10 or 15% of

**[05:09:51]** pollution, you have this resiliency, which I I think is very attractive. But this is something we totally don't understand. We have no idea why this is the case, but it's just a a very nice, I think, open question. For somebody out there, to look into. Okay. So just to wrap up, I think hopefully it's clear to people that you know, to some extent, some kind

**[05:10:17]** of madness or or collapse or some variant thereof, I think is inevitable as we move forward in this, you know, gen AI increasingly gen AI world, but but rather than just viewing it as a kind of it would as a dooms day kind of idea. I believe that if we're really, really

**[05:10:41]** careful, we might be able to come up with new ways to train generative models that actually avoid right, avoid or are resilient to these you know, gradations like, we have with collapse. But the key is that we need to exploit, right, the signal that is hidden, right, in this collapse sequence, and turn that into,

**[05:11:05]** you know, some new new way of of training. Right? So we saw neon as this one kind of scratches the surface. Of one potential way and I and I think that the key thing is that that that Neon opens the door to really thinking about not just model collapse and madness, but also really how we can be more data efficient. Right? With the data sets that we that we do have. Right?

**[05:11:26]** For example, if you have trained you know, I don't see why anybody wouldn't take any model that they are using today and just take another 1% of compute and improve the FID of of your model. Okay? But there's still, you know, lots of open questions. We're thinking about other people in the community are thinking about this this neon represents just one

**[05:11:51]** way of creating, you know, bad signals. That you can use to tune your models. There's a whole cottage industry of folks that are thinking of of either damaging models or damaging signals. In order to improve the performance of generative modeling. Is there a way to somehow do this optimally? Right? So get this optimal bad

**[05:12:15]** direction right, that when we flip it becomes a really, really good direction. Also need to understand this this prophylactic aspect meaning the fact that some of these methods that folks have actually can tolerate some amount of synthetic data, even in their, what they think is their real training data. This is, I I think, a really big open open problem.

**[05:12:39]** And then and then finally, know, we have just focused on generation as our ultimate task. But you know, there's a whole host of other machine learning tasks that folks would like to use models for. And and is really unexcited is and and madness actually impacts those kind of setups. Okay. Well, with that, I will end and say thanks

**[05:13:02]** very much for the invitation to be here. And happy to answer any questions. Thank you. Thank you, Rich. We have a few minutes for questions. If if anybody has questions, you can go to the middle. Yeah. Thank you very much for the interesting talk. I'm just wondering, can you give some very intuitive way to understand why the gradient due

**[05:13:31]** to synthetic data like, anti align with the real gradient? Because that sounds really counterintuitive to me. Because if you think of human as a, like, society of learning machines, it seems that I need to tend to disagree with what ancient sense say. Like, for the benefit of, like, human, like, developing? So

**[05:13:52]** but that's not what I do. So, like, I found it really counterintuitive. Yeah. It it it is counterintuitive, and it really surprised us I think it's easier to think about it in distribution space than in parameters. Space. So think in like score function, space and then just remember that in neon, it's just like the first order first order term in a Taylor series.

**[05:14:15]** Basically, if you take do Taylor series, the distribution. Basically, what happens when you when you do a mode seeking sampler, is that you are basically pushing down the tails Right? As I said, you're pushing down the tails of the distribution. And and pumping up the the the peaks or the mode of the distribution. And so and so basically, this this direction away right,

**[05:14:39]** direction away, basically tells you right, the direction that you that you need to go to push those to push the tails down and to push the mode up. And so basically, reversing that direction basically corrects. Right? Debias is basically. The distribution. And then if you just think that's basically how Sims

**[05:15:02]** works, And then if you think about if you think about with neon, basically, you take this argument that I just talked about in distribution space, you do tailor series, The thetas, the parameters of the first order terms, And then there are second order terms that are determined by how good the model was in the first place, second order and higher order terms, and you it's easy to show

**[05:15:24]** that if the model was good enough to start with, meaning close enough to the trueest data distribution, you can show that the first order terms dominate the higher order terms, and you can just basically do this parameter merge. So so hopefully that hopefully that helps. I see. A kind of more philosophical question. Do you think we should, like, disagree with other people more? Like, think your work suggest

**[05:15:47]** that? I would agree. Certainly, in certainly in like dialogue and online dialogue. Right? The you know, another related idea here that goes way back is the idea of echo chambers. Right? Which is a human human idea. That that that people proposed. As soon as social media came out, people were like, uh-oh. We're gonna end up having echo chambers where people

**[05:16:11]** have, say, certain political ideas or people who love Taylor Swift right, and don't like Madonna, gonna hang out and their their ideas are gonna be biases are gonna be reinforced. You can really think of model collapse and as an echo chamber of AI. So, yes, you should disagree with people as much as you can. Very

**[05:16:34]** interesting. Thanks. Just a quick question. So w is the hyperparameter Yeah. W is a hyper I should have mentioned. Just a hyper parameter that you could search for using some kind of, say, grid search. Okay. But, maybe can you give some I mean, theoretically, I mean, it should depends on the number of Yeah. Very good, but

**[05:16:59]** yeah. So there's a hyperparameter hyperparameter w. That determines performance. We have rules of thumb, but no theory as of yet. That that's that's a good question. That's an open yeah, open scientific question. Thank you. Alright. For this oh, maybe okay. Let's take one more question, Adan. Thank you for a great talk. I have a

**[05:17:28]** question. Is it true that you have added this synthetic synthetic data that was generated from the same model throughout the training loop. Correct. In the in this method, in neon, it's the exact same model. So have you tried adding, the data from the different model? Great question. So the question is, what about

**[05:17:52]** using synthetic data from a different model? It's kind of like a transfer learning kind of thing. It also works. Also works. Not quite as well, and I think you could see that if, you know, if you really rely on this, like, degradation signal hypothesis, then the the no better model than the very very model you have. Yeah, it transfers really quite well. Okay. Thank you so

**[05:18:15]** much. Question. Alright. Let's, thank Rich. We have another round of applause. Thank you. So our next speaker is Matthew Viar. He's a professor of physics, at John Hopkins and EPFL University and more recently, he has focused his research on understanding how deep learnings

**[05:18:45]** work, in particular, his lab made very interesting contribution to how compositional and hierarchical structures in data help the learning process. So today, we're gonna hear about some of the results in the context of language models. Now you can hear me. Yeah. So, so I'm very happy to be here. Thanks

**[05:19:15]** in Rio. Thanks for having us, and it's a beautiful workshop. So it's great. And I'm also very excited to tell you about this work. Because I think it's engaging with the fact that's impacting all of us, namely neural scanning laws, so so the idea that if you put more money, more parameters, more data, you can, in a sort of predictive manner, increase the performance of,

**[05:19:39]** LLMs. Which has completely, you know, impacted the field and led tech companies to those massive investments that, you know, we're witnessing the the change of technology. And despite that, for for theory, we really have no clue what's to, you know, what controls those I think Bruno nicely summarized it this morning. You have lots of very beautiful theory on kernel methods

**[05:20:02]** and so on, I which in in some cases can be very useful, but my contention is that for languages, it's not really a good way to think about it. And what we are trying to propose here is actually a theory where you would be predictive. Predict the exponent based on the statistics of languages. And this is the work that's done with very talented young collaborators, Francesco

**[05:20:24]** Cagneta and Allan Raventos. And in collaboration, with the group. Of Surya, in Stanford. So the general question, no. Is about learning, you know, language from exam. And it's an old question for for linguists. And the question really here is what they call creativity. If, you know, a child is exposed to sentences,

**[05:20:48]** how many sentences does he need to be able to create new sentences that it never heard before, that will be correct grammatically. And And, Ram Shamsky, last century, you know, famously said that it may be impossible. That you need grammar needs to be innate. And what I find very exciting is that with LLMs okay. Now we we see that they can amazingly well.

**[05:21:13]** So it's possible. But you can really you know, it offers new handle to to study important questions like, you know, what are actually the statistical correlation. That are harvested by those LLMs? How many data do you need to learn what? Okay. So we know, what's the one objective that works to learn languages, and you you guys all know about next token prediction,

**[05:21:36]** but I I will still have this slide to introduce some some key concepts. So you use the chain rule. So t will be the maximal context. Let's say, the size of a paragraph or something like that. X I would be token in position I. And what you use is the fact that the joint probability can be written as its product p of x, you know, p of x one, p of x two

**[05:21:59]** knowing x one, and so on. So note that are my notation for context between one and token n minus one. And then what you do is you train a model, say, a large language model, to maximize the likelihood of your observation. So when you take the log of this product, you get a sum a sum of loss l, sum

**[05:22:23]** of l n, and l n is the loss associated with a a context of size n that vary between one and t. So this quantity l n will be very important here. And the other thing you need to know is that this cross entropy, even if you have the best it it cannot go to zero. At best, it can go to the conditional entropy, which I will call h n.

**[05:22:47]** So conditional entropy of the next token if you know n tokens before. That's, again, going to be very important here. Okay. So what we have to learn then is this probability, conditional probability of x n if you know the context before. But here comes a very common, you know, curse of dimensionality problems that if you are trying to histogram this distribution,

**[05:23:12]** it would be essentially impossible because the number of you know, context of size and growth So it should be impossible to do generically, and it is for unstructured data. So it means that learnable data have a lot of structure. So what is you know, the structure of language that makes it learnable And how is it are vested by, say, large language models?

**[05:23:37]** So one aspect that many people believe is actually key, and that's the name of this conference, right, it's representation learning. And in particular, the fact that it's also true for CNN and images, but that those net, as they learn what in physics or physicists in the audience, we will call coarse grain file So if we describe a liquid, we're not we it's not useful to track all the position

**[05:23:59]** and velocity of particles. Whether you want to have fields like pressure, velocity, and things like that. So you build variables that do not depend on details. And, deep nets and So here, I like to give the example in LLMs, this golden gate bridge what you see that you have linear combination of neurons that

**[05:24:23]** respond very specifically to having the notion of golden gate in the sense. But this is very robust. It does not depend on the details of the syntax of the sentence. It even doesn't depend if it was a, you know, multilinguage model. If it's said in Chinese or said in English, and if it's a multi model, you also have vision. If you show a picture of the Golden

**[05:24:46]** Gate, you trigger the same linear set of of neurons. So that's also a question. You know? How do you actually build those coarse grain variables What structure in the data enables it? Okay. So then that leads to how do you actually quantify success in those neural scanning laws? And in this talk, I will just talk about one of them,

**[05:25:10]** which has to do with how your performance, your test loss depend on the number of data If you have lots of compute and lots of parameters. Your data are limited. So the tesla goes like b to some exponent alpha. Okay. So that's my question. What controls this alpha? So Okay. So this talk is cut

**[05:25:32]** into two So the first part of the talk for the physicists, it's like thermodynamics. I will make a sort of simple assumption and from it, we'll be able to make predictions that we can actually test natural languages. But this this assumption is simple to state, but why it's true is not obvious. So in the second part of the talk, I will actually talk about a microscopic model where we

**[05:25:55]** can understand why this assumption is actually correct. So So let me introduce the two, what I will argue are the two key properties of natural languages that control their the neural scaling load. And the first one is the fact that you have long range correlation between words or token in text. Which is well known for for a long time. So,

**[05:26:20]** for example, you can define this matrix, you know, if I have token, mu, what is the probability that I see token new at a distance n. I it's a matrix that depends on the number of token but you can look at norms of this matrix. And whatever norm you look, operator norm, forbidden use, you find the same result. And here, it's shown for the two data sets that we're going

**[05:26:42]** to study, tiny stories, which are sort of fairy tales. And WikiTek, which is a curated version of Wikipedia. And what you find in both cases is that you have poor low decay of those correlation. And for Wikitext, it sort of breakdown after 30 or 40 tokens. And this is actually the scale that I consider. Which is a few sentences.

**[05:27:06]** And that's where we can test our theory. So you can measure those exponent, and you find that the depend on the dataset, and I call this exponent beta. How's the correlation decrease with context? N? So that's the first key quantity. And from it, we can extract an important notion which is if you give me a given training set of size so in this talk p the size of

**[05:27:30]** the training set, on which context length can you actually measure correlation. And that's what you see in this simple example. So that's okay, that's for Shakespeare data, and you see the polo correlation in Shakespeare. In color, you see you know, trying to measure those correlation with more and more data. And if you don't have much data, you do very And you see visually that there is a scale.

**[05:27:53]** And this scale is readily obtained by just comparing sampling noise going like one over of peak. And the signal I told you about that goes, like, n power minus beta. And from that, you get a scale. We call it n star of p It depends on the size of of the training set. It tells you on which scale you can actually measure correlation. And so here come our key assumption. Our key assumption will be

**[05:28:17]** that machines they cannot exploit context that are much larger than this NSA star of p. But if you have very good machines like LLMs, and not kernels, they can do they can work essentially optimally on that scale. What I mean by optimally will be stated in the coming slide. So the second property we argue is very

**[05:28:40]** important is this conditional entropy. That I told you about. Right? What is the entropy of a token if I know n tokens just before? And And it seems that it's very hard to measure because again, it's cursed by dimensionality. Here we're going to use that LLMs and do not seem to be cursed by dimensionality. So in particular, we will use the fact that I told you already that this

**[05:29:03]** conditional entropy has to be the optimal of l n, if you give me a machine which has a huge capacity, so let's take the capacity to infinity first, And then you train on a huge number of data, and you are fixing the context end. Then this loss l n should converge. And what it should converge to is precisely this And that's

**[05:29:27]** something that you can actually test and perform empirically. And that's what you show in all those plots. So this is l n. This, this loss for a contact end. So the effective is n and the different colors what happens when you increase your training set. And what you find is that if you are at small n Zoosk curve actually

**[05:29:49]** converge to a well defined value. And so it should be our conditional entropy. And then we double check that this limit actually does not depend on the architecture that you use. So if you use GPT style, you know, LLM or Lamma, or even if you look state model like Mamba, you actually find the same value. And what you find, again, on the scale of

**[05:30:11]** 30, 50 tokens, is that this conditional entropy is well fitted by a power low decay with some exponents that depend on the training set, but you that you can measure. And so here's a theory slide I our assumption that you can perform optimally for deep architecture on that scale means that the test loss, if you give me you know,

**[05:30:34]** if you have a very large contact t t, but you give me a finite training set, you will only be able to as a language on this context n star of p. If you do it optimally, then your tesla should be given by this conditional entropy on that scale. And the good thing about this theory is that it's very predictive, because n star of p you know how it behaves.

**[05:30:58]** And the entropy goes like n minus gap. Gamma. So you immediately get that your neural scanning logs alpha should behave like gamma over two b. Beta. There's another prediction that think leads to even much more stringent prediction. Which is very common in physics, but maybe less usual in other fields. It's called scaling collapse. The fact that a function of two variables like

**[05:31:22]** this test loss that depends on the context and and also on the training set p, is really a function of one variable in this guy. So comes from the fact that it it has to have two asymptotic behaviors and a crossover between them. So imagine that, you look at the case where your data the number of data is small. Then what will happen is that the context and

**[05:31:45]** not matter. You see effective context on which you can harvest data is n star of p, which is much smaller. And therefore, you recover that the test loss should just depends on this h of star of p, which is p minus alpha. On the other hand, if you have lots of data for finite context, at some point, this data n star of p becomes larger than n, but there's no

**[05:32:09]** no data to explore on larger context. So you will just saturate performance at the entropy and context end, which is just n point for minus gamma. So what you get ultimately by putting this together is that your test loss, that's a function of two variables, should really be a power of n time what we call a scaling function. Something that only depends on on this ratio here.

**[05:32:31]** That behaves as a constant for very large p and as a parallel for small argument. Okay. Now comes empirical test. So the the first prediction is just predicting the and, okay, the scale at which we we we work we are in the data limited regime, so we have things like 1,000,000,000 parameters, 10 per eight, a few 10

**[05:32:56]** per eight data. So number of data is actually seen on the x axis here. And what you see in color is essentially the classical polo. How does it test loss set? And what you see as the dotted line, our prediction without fitting permit. This has no fitting parameter. We measure those two

**[05:33:18]** exponents gamma and beta. We deduce what alpha should be. And you find that for Wikitext, it works remarkably well. And for tiny stories, it works pretty well. Actually, as you increase the maximal horizon t, the maximal context t seems to work better and better. But what's really think, is most convincing is this non trivial prediction of scaling collapse. So here, what you

**[05:33:41]** see is those test loss l n on context n as a function of the size of the training set b. So the different curves corresponds to different colors which corresponds to different end. And that's where our theory makes a very stringent prediction. If we rescale the axis, in a way that's not fitting parameter, it's completely fixed by previous measurement. All those curves

**[05:34:03]** should collapse. And they do. They do both for tiny story and for Text. So I think that's the strongest support that we are on the good track. Okay. So, now comes the microscopic theory because the is, why does this assumption is actually correct? Why is it that you know, once you start to measure correlation, you do essentially

**[05:34:28]** optimally? It means that you beat the curse of dimensionality. So what's going on? So what is the mechanism whereby machines do well on that scale? And for which data structure is it possible? Because for generic data, it's not possible. You're cursed by dimension. So Okay. So the game we are playing as physicists is to think about synthetic

**[05:34:52]** models of languages. We're inspired by the work of linguists I mean, Norems Shamsky in particular. And they have you know, the notion that underlying the linear structure of text you have trees. I mean, that's a very old idea, much older than I'm sure. And then that you can describe the statistics of text by describing the statistic whereby latent variable that you don't observe on that tree

**[05:35:18]** can give rise to strings of latent variables. That's context free grammar. So we'll be playing with models of context free grammar, and it's an idea that has been also very impactful for computer vision It's called pattern theory. It's the fact that underlying images, you also have trees. And images of a grammar on their of their own. So there have been works, you know, looking at how

**[05:35:40]** LLMs learn context free grammar, But who's works considered complicated context free grammar where learning could not be understood, Postmortem analysis of the algorithm done was studied. So here, we want to make it simple, and we are actually going to use in conjunction two approximations that we have proposed in some literature. So first one, our tree will have a frozen regular topology.

**[05:36:03]** The second one is that production rules how one latent give rise to a string are going to be random. And if you do those two ingredients, then you can compute all correlations in this problem. And really understand how and test your ideas of how LLMs learn learn such models. Okay. So we call it the random hierarchy

**[05:36:25]** model. So it's a context free grammar. The key ingredient is that my mouse here? Yes. So each symbol here give rise to strings. So let's call s. The size of the string. What's really important is that, say, b can give rise to d f, but also to other strings. In this model, the parameters that control that is m. So b could lead to m

**[05:36:49]** different strings, And those strings, we call them synonyms. Because they all mean big How do we choose those strings? Well, we choose them randomly. That's the point. And we also choose them as set that have, no overlap. So say a and b cannot give rise to the same stream.

**[05:37:12]** There's another interesting quantity in a model like that, It's a fraction f of the rules that are used. For example, d f exist as a string. But many strings do not exist. And this fraction f depends on the vocabulary size. And we can manipulate a model like that essentially is compositional, so you see you don't see the latent

**[05:37:34]** visible at the end. And it can generate it's a language that can generate an immense number of data exponential in the context, the maximal context end. And so you can study what we study at the time was last token prediction. What happens for a machine that's trying to predict the last token knowing what comes before. Okay. And so the first point I want to make is

**[05:38:00]** that simple model like that captures the two key properties I told you about in languages. And again, the first one is well known. It's well known that if you have tree like models like that, they lead to poor correlation, poor low correlations, of symbols at the bottom. Essentially, what happens is that every time you move along this tree, you can ask how to

**[05:38:23]** variables visible or not are correlated in a tree like that. Every time you move along the tree, you the correlation diminishes by a quantity that just depends on m. This number of synonyms. And so correlation decay exponentially with the distance on the tree, but the distance real token space is also the tree. And at the end, it leads to a

**[05:38:45]** correlation that decrease as a ball of distance. So you would have to trust me on that. This is which can be controlled. It's not universal. It just depend on m, the number of synonyms, and as the branching ratio of the stream. Okay. So it has polar correlation. It also has a conditional entropy that's And so so you ask, what is the entropy of this last token that you don't see here?

**[05:39:11]** If I condition to knowing everything that comes before? And what happens is that you don't really doesn't really matter everything what comes before. The only thing that matters are actually those latent variables that I surrounded by green. Only them are informative in terms of what can happen for the hidden So And what happens is that at every level you consider

**[05:39:33]** the fact, for example, that you've seen a, restrict the number of you know, symbols that are actually here, written as b, by a factor f, you know, the fraction of rules that And at every level you consider you always have this factor f entering here. And so what you find is that the entropy as a function of context is just f to the power l,

**[05:39:56]** the and of the tree. I mean, there is a floor. I'm not going to enter into details. And that's just again, the distance add along the tree being, you know, logarithmic in the context length you get a power load. So in this model, it's correct that the conditional entropy is a power law of con Again, with an exponent that you can manipulate at hand.

**[05:40:21]** So Okay. And in this model, we can really understand what is the mechanism leads to learning. Why is it that our main assumption in the first pack part of the talk is actually correct? So So, again, what you're trying to understand is a correlation between a long engram and the last token. And, again, it should be cursed by dimensionality because the number of engrams is immense. You never see

**[05:40:43]** twice the same. If n is large. What's actually saving you in a model like that is that you don't, again, care about the end gram, you just care about those those green latent variables that I surrounded here. So, if your machine can learn to build those latent variables, then you're saved. And actually, you can learn them precisely because those latent variable

**[05:41:10]** controls the correlation. So, for example, imagine that you're looking at the correlation between this string h g and the last token. Those correlation only depend on the latent d above. Synonyms have the same correlation. And so it means if you give me enough data, I can measure those correlation It's a signal to noise argument. And cluster together those you know,

**[05:41:33]** those strengths into latent variables. And I can do it hierarchically. If I know that this is e and this is f, I can again look at correlation between those latent variable and the last token and build those latent hierarchy So it's hierarchical cluster. So that's a mechanism to actually build those latent variables that are cause during variables. They do not depend on

**[05:41:56]** details on what were the exact production rules. Behind them. So Okay. So in a model like that, what happens is that if you do next token prediction, you start to learn this production rule from the bottom. So you first learn production rules that are close to the last token and that are at the bottom of the tree. And as you give

**[05:42:21]** more and more data, you start to learn higher and higher level variables in and you and further and further away. And, actually, the bottleneck in a model like that is to cluster together synonyms that are the furthest away from you. And what really matters is a correlation between strings and token in a model like that.

**[05:42:44]** But in those models, it's scales in the same way as a token token correlation. Third, the end, what you find is that this assumptions is the fact that when you have enough data to resolve correlation, that's when you can actually completely learn the model. Is true. For the simple models of context figure. Okay. So, actually, that's something that you can

**[05:43:11]** test in those synthetic languages. You can vary parameters and what I told you before is the fact that we have predict prediction for neural scanning loss for this exponent. Alpha, and it should depend on the parameters of the model. And so that's what we test here. M is the number of synonyms. VISO, I did introduce it. It's the size of the vocabulary. Taken to be the same at every level.

**[05:43:33]** And what you can compare our observation what our scaling loads on an LLM trying to learn the synthetic languages. Compare compared with, you know, theoretical Okay. So, so here are my conclusion slide. So what we propose is a theory of neural scanning laws that relate the scanning laws to the exponent to actually

**[05:44:02]** properties of natural languages that you can measure. I told you that there are two key properties token token correlation and this conditional entropy. On context length. N. And that these proper properties appear naturally in contact in simple context free grammar models. And that leads to a mechanism for this hierarchical for for building coarse grain variable, which is based on the sort of hierarchical clustering

**[05:44:29]** approach. So okay. So if I have two minutes, we were also asked to to give some some vision of where it's going. And, and I just wanted to mention, in addition to you know, what was discussed this morning in terms of why is it that interpretability understanding really what LLMs are doing is important. I see

**[05:44:51]** and I completely agree with what was said, but I see another another argument for that. Is the connection between what LLMs, how they are representing languages. And how our brand are representing language. And the as time goes, there are there is more and more evidence that those two representation are closely related. So I think that

**[05:45:14]** once when you do theories of how LLMs, you know, represent language, you're also doing neuroscience, at a brain level where there is very little theory done, but, where there are more and more facts. So so I think this is a very, you know, interesting field for the future. And, and how and I didn't connect that to my

**[05:45:36]** talk, but something that I find very interesting is that example, when they map LLMs to brains, they find that as you train better LLMs, you start to map better at you know, low levels aspect of the cortex, like auditory cortex, for example. Is and you train more and more this mapping starts to occur at more

**[05:45:59]** and more abstract level. And even the simple models I told you about, it's also true. If you give me more and more data, you learn rules Okay. Thank you. Alright. Yeah. Use the microphone in the middle if for questions. Thank you very much for the talk. To me, it's really exciting to see the universality curve I mean, the function f that everything

**[05:46:30]** collapses to in the first part of our talk, But, you know, in physics, that usually happens near phase transitions, or at least there needs to be some CFT I mean, any, like, scale invariant theory So, like, do you think there's some kind of scale invariant theory or a phase transition like, it seems that language is happening near this kind of place. Well, I I would think that, this sort of

**[05:46:57]** scaling collapse here also occurs in those simple models of language, artificial ones that I told you about. Uh-huh. Uh-huh. And and it's so it's also true in this class of model, but the physics of it is a bit different from crude usual critical phenomena. Where you can have local interactions that that's temperature lead to, you know,

**[05:47:20]** polo correlations. Uh-huh. You need fine tuning in physics to see polo correlation. But in data, languages, you see it all the time. You do have you know, parallel correlation of tokens or words. So I think the, you know, I don't think it's because the world is fine tuned to be critical. I think it's because you have another rational for that, and I think the understanding that you have underlying text street.

**[05:47:44]** So but still, if you think about three at this level, you still have the scaling collabs that emerge. Thank you. Thank you. There any other questions? Alright. So we have an half an hour break. You can and both Rich and Matthew are in the the space if you have questions to talk to them. And

**[05:48:07]** then after this half an hour, we're gonna have the panel discussion at three So, let's thank Matthew with another round of applause. Yeah. And if you are presenting your poster in the later poster session, use the break to hang it up here come take your seats. And for five of you, those seats are on stage. You know who you are. I'm

**[06:19:54]** with you. See you. First time I got Alright. I you guys ready? We would Yeah. Alright. Alright. Everybody, thanks for sticking around for the panel. I'm Jamie. One of the organizers here. Yeah. Honestly, really loved all the all five talks we had, and I'm jazzed

**[06:21:38]** to have this panel here in particular to ask questions to because I mean, as we saw from the talks, I all these five researchers have like, well developed, but very distinct research team. Tastes. Different approaches to developing a science of deep learning, that I I think are are are all complementary and and really inspiring. And I'm I'm, you know,

**[06:22:03]** excited to explore this. So this will be a panel gonna run for like an hour ish. Towards the end, we'll have audience questions, so you can have, you know, have questions germinating, they can come out at the end. Alright. So, and for anyone who wasn't here for the talks, the the, panelists here are, David Bauer, Julia Kemp, Rich Berniak. And Matthew Vaiart and Jeremy

**[06:22:30]** Cohen. Alright. So, first question, we're gonna start with an easy one. In our field, what makes good science? So, yeah. Like, you know, we all we all want to understand this We all want to understand deep learning we want some kind of a scientific theory of And clearly, there are ways to there there are attempts to make progress,

**[06:22:56]** avenues progress that that that seem to be working, that are more promising than others. Like, what makes good science? What do you look for? In a paper? What makes you excited about a new result? I mean, the goal is to get at the truth. Right? So, like, like good science is what's true. I think that's more important than anything else. I mean, some ways that you can tell that it it sort of possible to, like, fool

**[06:23:20]** oneself into, like, thinking that, like, like, you found the truth when you haven't. And so I guess that's there are other, like, signatures of like good science. But, like, know, like, which I mean, there are probably a lot, but, like, just to name one like, one sanity check that you you're on the right path is when you can for example, like, if can make like predictions, like in Matthew's talk, like, showing, like, the model, like, makes this precise prediction.

**[06:23:46]** That's, like, you know, an like like something has gotta be going right for that to be true. So that's a good signature. Hello? So I would just be repeating what actually you said this morning, which resonated with me that good science has, many forms. And, and if you think about, you know, what you were introducing, how do we a good paper should it

**[06:24:11]** have the theory and the algorithms that works in practice and and I think, no, it's much more of a continuum where, you want to have theory and practice that two ends of a continuum and, and we work as a community to to make it work. So so very good work can can be there at, very different location in this continuum. And also with different methodologies

**[06:24:36]** It could be, as you said, theorem, is one approach, but but there's another way to try to be rigorous, which is maybe it's not your aim. You propose arguments, but then you have to be very rigorous in terms of how you actually test it So I think that's already that's also very variable, and it a it would be very nice that, yeah, all those, you know, all those different approaches are

**[06:24:59]** considered and Yes. I'll just add there's a theory of science Right? So, we would like any deep learning theories to to basically, hew to those proper basically properties like you'd ideally like to be able to have hypotheses that are falsifiable and ideas like that. I think the

**[06:25:26]** thing that I look for most that I think was in that it should be actionable and that's just because we are a we are a small little tribe in a very big machine learning world. Most folks who come to ICLR are not. Here for the theory. Right? They're here for the

**[06:25:51]** benchmarks. Right? And so I think the more that you're theory can can be actionable by people who are chasing those benchmarks, the more that it's likely to be, have an impact on the field. Michael, for this Yes. So, to add to what my colleagues have said,

**[06:26:15]** I see I see two pieces to science. Right? There is the understanding science and then there is the nice part where we can actually as you say, be actionable or predict something. Right? And, I feel both pieces are very important and often I think a bonus that you get when you do the understanding pieces that often something actionable actually comes out. Right? And

**[06:26:38]** that very nice. I do see, a bit of a tendency, so I'm not you know, if you steep in the science community more, there is a bit of a tendency maybe to do the science because we can. We are able to compute on Gaussians, Let's just put a Gaussian on the data. So that's a temptation that I I I feel in my science colleagues, and there it is, I think, important to ask, you know,

**[06:27:02]** am I actually modeling the truth or the phenomenon I want to explain. Right? So and and this is an important you need to not just do it because you can. Think. Right? You better, do it because it will explain something. So as the last person, I I don't have much to add. You know, science should be rigorous, should be actionable. I I think I I tend to advise

**[06:27:26]** my students to think about ideas that might be productive. That might be good building blocks that you could build other ideas on top of, I think that's in addition to all the things that that are talked about here. But there's a human aspect to to what makes good science. So okay. I I I there's a question I wanna I wanna piggyback on that before I get

**[06:27:58]** to the next one which is all of us in this room, I'm sure, have felt precisely the pressure that that Richard is pointing out That in order to be relevant to the people outside of the room, you know, we we we better help them beat soda. And and, like, great if we do, but Jeremy says something in his talk that that spoke to me and I'm sure to others,

**[06:28:23]** that, like, we can't always you can't always do that in one step. So so so yeah. Sorry. I I wonder how you guys resolve this for yourselves and what advice you would give to, like, students who are who are trying to do something relevant, trying to get conference papers in, you know, how do you manage this this these two tensions? And and what's what's philosophy? Yeah. Good question. Yeah. So I think I

**[06:28:46]** would probably like, tend to, have dis I I would maybe disagree with the the the argument that we should try very hard to be like, to make give actionable guidance for practitioners. Because I think that, like, I feel like we're just in a deep learning we don't understand deep learning very well. And like most of the time, you just can't I feel like the set

**[06:29:13]** of things that we can currently give actionable guidance on is minuscule relative to the set of things that we will hopefully one day be able to give actionable guidance on. So I think it's better to, like, not there is pressure, and I think there's a vicious cycle. I think there's the following vicious cycle where, like, theorists like, see talk to practitioners and realize that practitioners don't care about theory. And then

**[06:29:37]** they were like, okay, I need to make my theory more relevant to practitioners. But then the practitioners in turn, what they do is they read these and then they implement it. And it doesn't work as well as their baseline. And then they're like, oh, theory doesn't work. I think there's like a vicious cycle here where, like, I think that I think what I would sort of recommend is,

**[06:29:59]** like, just saying to the practitioners, like, sorry, like, I Like, and just sort of viewers just sort of sticking to their guns more. I'm using theorists in the broadest sense of the term, like people who work on understanding singing to their guns and saying like we're gonna do the theory and then when the theory is done then it'll be useful. If you if you are looking at other sciences like physics, I mean, and would not have

**[06:30:24]** published anything and and still yet, you know, this giant technological impact at the end, but, but again, I think we work as a community. And and the same person doesn't need to go from very big ideas to to application. So I, I would completely agree with that. Yeah. Yeah. I don't have much to add except you can always point out the success stories. Right?

**[06:30:51]** Okay. So theorists think, they do their thing, and then we get things like resonance. Which you might argue maybe comes from petitioner, but maybe it comes from trying to understand why the gradients remember, this whole thing in 2016, gradients explode gradients shrink, everybody thinks about it. Boom. ResNet comes. Right? So, clearly, it's a success. So I think, even practitioners will, I think, admit that theorists diffusion models.

**[06:31:14]** I mean, come on. Right? So I think there's enough success stories to have a justification for our slow approach. Right? Not on a three month deadline. Sure. I I wanna add another thing, which is so in May and maybe my my area is a little a little different, but even encouraged the theorists to think this way. Which is that

**[06:31:37]** one of the things that we can do when we're looking at fundamental questions is also open up the space of new applications, new problems that you can solve that people didn't think. So maybe diffusion models is one of them. Right? But new problems to solve that people didn't think was what they were trying to do, but if you take a new look at it, closer to my area, there's this area

**[06:32:01]** of model where you have a model and maybe you understand the structure well enough that without process, process, you can customize it in different ways. And, and and because of different properties that the distribution has or different things. Right? And and, and it actually became this of practical techniques

**[06:32:27]** if you go to Hugging Face I think something like third of all the models on Hugging Face are customized models that use some of these lightweight techniques that came out of like, a mechanistic understanding of what what's going on. But it's not it's not something we get credit for, like, moving state of the art forward. It's a new

**[06:32:50]** application. Something different. But I still think I I still think it was a really substantial contribution. To open it up. So you know, So so so one of the most exciting things about this this science that we're that we're in that we're hopefully building is it's really nascent. It's not it's not clear what

**[06:33:20]** this theory we're gonna find is. It's not clear what the understanding will look like or or, what it'll be useful for. And that that's wonderful, and I I think it inspires me people here. So so I'm I'm curious to hear your answers to the question of well, what are we what are we trying to do here? Right? Because like clearly, not everything is the science of deep learning.

**[06:33:46]** The boundaries are really vague. The the the goals are the goals are really big. And, like, if you were to articulate maybe, you know, in a way, again, trying to, like, inspire a young graduate is or something to get interested in this, like, what what are we trying to do here? And and and, like, what are what are the highest ambitions? What are the scopes? And what should we be aiming for and, like, work

**[06:34:10]** backwards to decide what to do today? Yeah. I guess my answer is maybe I think not everybody would agree with this answer. But I guess to me, like, and this might appear to contradict what I said last on the last question, but it doesn't actually. To me, the the ultimate goal of deep learning theory should be to drive practice. That's the end goal. The end goal is that when

**[06:34:37]** people are doing deep learning, that they are talking about theory. They are using theory to guide what they do. Maybe it's not gonna tell them oh, set the learning rate to like point o four two. Like like, it's not gonna like, necessarily tell them exactly what to do but they're gonna they're gonna, they're gonna, they're gonna, they're gonna, they're gonna, they're gonna, they're gonna, they're gonna it should be valuable enough that they naturally find themselves using it. When they go about

**[06:34:59]** doing their deep learning. But, like, that's the long term goal. To get there, we first need to build the theory that's capable of doing that. I think a not a different a totally different answer would be like, oh, the point of theory is to like, understand. But like to me like understanding is kind of ill defined goal. And like, it's whereas like,

**[06:35:22]** like, like it it's not even clear It's not act like it's not actionable. How do you know if you've how do you even measure it? You've under So like the the me the ultimate goal is to be driving practice. But to get there now, need to focus on building the foundations first. So in terms of understanding not being clear, I guess, if you just state it like that, yes, but

**[06:35:46]** then you can if you try to clarify the question and ask, for example, I mean, that's very subjective. What questions are driving you? I inform you one question I'm fascinated about is an old question. You know, generic data are not learnable. What in the structure of data make them learnable? And why is it that deep net are actually really good at it. You know? So so I think it's once you make the quest question

**[06:36:08]** specific and your five drive toward them, then then I think you can this notion of understanding become meaningful. In addition to those kinds of question, one aspect that I find very fascinating is Now, I mean, this and relating to the works that, I mean, some of, people here are really working on, like, interpretability, how syntax, semantic are represented

**[06:36:32]** in, language models. I was starting to mention that in in the talk, but, if you you know, if you do theory on trying to I mean, of all, it's a fundamental question in itself. How can a machine learn to speak? How does it generate, you know, good language? And I think linguists are fascinated by that even if it was just a machine. But then now we are finding more and more evidence that

**[06:36:57]** representation in the brain are similar to the machine like Lina. Last month, there was a paper showing that king minus man plus woman is queen. That's is is when known already in World two vec. Actually, it's also there in our brain. I mean, so so I think it's another justification that if we understand is not machine specific. So it's not

**[06:37:22]** just about understanding what specific man machine, it's something of nature. So I think, I think I forgot the question. Because I was thinking about these great answers. And and just thinking where's my t shirt? Just so disappointed that I have a t shirt. I'm a medium. So so I'm not sure if I'm not sure if this addresses the question, but,

**[06:37:51]** maybe it addresses the the previous question. But I I think it's important like really important to like keep in your mind, like differentiate between what I would call, like, a theory driven field and an an example of a theory driven field is communication Everybody has a phone, Right? Five g, six g, seven g's

**[06:38:15]** next. This field is is just built wholeheartedly on on information theory. Right? Which is rigorous branch of mathematics. And and the important thing is in a field like that, understanding can be total. Like, and and people are building systems that are within epsilon of, like, Shannon capacity. Right? So theory and practice

**[06:38:41]** can really really go together. And I think some people come into the theory of deep learning world thinking that it's a little bit like that, when I would argue it is much more like chemistry or neuroscience. Right? Where you'd have this incredible complexity where understanding really may never be truly reached may never be truly reached but

**[06:39:05]** that's not just a that's not necessarily bad. That's like means there's just tremendous opportunity for a light like a lifetime of work. And so to me, I think folks who work in deep learning theory, it's really about, like, joining into that that that journey. Yeah. So I don't have that much to add, but also there is a difference, I

**[06:39:28]** think, between science of deep learning and theory of deep learning. I don't know. Also, I don't remember what you asked. And I already got my t shirt. Thank you. But, it's different. And I think for us, it is important to bring the scientific method to this field. Right? Because indeed there is all these other rooms that are chasing the benchmarks, and perhaps, you know, are neither motivated nor

**[06:39:53]** set to apply the scientific method, which also is about admitting you know, what fails, basically, which is not so popular in the other rooms. And I think this is you know, as a scientist, that's what we have do, scientific method, write down what works, write down what fails, understand failure modes is one important thing, and, this is also upon us as a community of scientists in this field

**[06:40:15]** to do, I think. So I I I think that I I like this question a lot. I think that I I like the sentiment. Yes. Well, you know, or or something like that. I I've been mostly thinking that, the the actually, the organizers are amazing because unlike any other workshop I've seen, they seem to have ads as well. And so I'm I'm wondering where these ads come from.

**[06:40:37]** So but but, the the so I'm gonna echo one of the sentiments that I think I it resonates with me you know, we are we're in a messy field. But we are also in an ancient field. Because the question of what is thinking

**[06:41:05]** is as old as philosophy. It's a 5,000 year old question. And and we are at this unique moment when suddenly, we can analyze the question of what is thinking what is learning, what is reasoning, what is cognition, in a new way that that the old philosophers could only dream of. There's there's this old treasure chest

**[06:41:29]** of questions that used to be non scientific And yes, they're very messy, messy questions. Know, what is language? You know, what is what is intent? What is agency? You know, what is meaning, what is belief, Right? They're messy, messy questions that used to be philosophical almost religious questions. But actually because now we

**[06:41:53]** have reproducible system, mathematical systems that exhibit a lot of these behaviors. We can we can start the process of taking these old non scientific questions and making them scientific. So so I'd echo the sentiment that, yes, it's a messy empirical field, but that's all also where a lot of the possibilities, come from. And

**[06:42:17]** so, yeah, that's so I think that's maybe that's the I think, I would point out. Yes. Sure. Ask and you shall receive. Yeah. Those were all really inspiring answers. David, your last, comment reminds me of a of a quote often bandied around by like sort of resentful philosophers that everything is philosophy until it becomes useful and then no longer

**[06:42:43]** considered philosophy. And and and so it's so exciting that we're on the we're on the cusp, you know? Like philosophy is more things are becoming empirically tractable. And and they're they're bleeding into science, and it's great. Okay. So so now, you know, we we all agree that that this is an important and interesting thing to be doing. My next question is,

**[06:43:06]** how should we organize ourselves to do it? Right? Like, I I I I've I've I've never met a single experienced academic who doesn't have you know, one or two minor qualms about the way academia is organized. You know, or like the conference system or the review, you know, what whatever. Right? So so my so my my question my question for you guys is, if you could like,

**[06:43:29]** imagine someone just gave you total power to you know, and license and encouragement to, like, lead a huge collaboration, restructure the fields, you know, organize us so that we can make progress on these questions, How should we do it? Right? And what should we be doing differently than we're doing now if we had to reimagine it? You wanna see? Let's actually start with David. And go the other way. I have to give an answer to this one. Alright. So I so I I

**[06:43:52]** I'm happy with the situation. Field. So I Okay. If anything, I think that so I I think that the traditional for this type of that we're facing here in this room, I think the the traditional academic perspective is probably pretty productive I think it's a time for creativity. It's a time for new ideas. I think academia has traditionally set up

**[06:44:16]** to encourage new ideas by having every every corner of academia you go to you find people thinking differently And some people, like, I, have conversations with some professors, some postdocs, who worry that people use different language to do different things. There's some disagreement of what's true and what's not and so on. Right? There's because because our field is so fresh, And

**[06:44:38]** they they they wanna impose more order on it, They say, let's you know, let's let's, like, put an end to this. I think that some people are getting funding, which they shouldn't, because you know, people don't understand the consensus whatever. Right? And I'm not I I don't not sure about that sentiment. I feel like I feel like we don't know enough that the the field is so fresh. It's time for creativity.

**[06:45:01]** That it's okay for there to be a lot of different ways of naming things and lot of different ways of looking at the same phenomena. And when when people discover something productive, when that idea is so good that the idea will speak for itself. The idea will spread. Right? Other people will adopt the language. And and and the fact that maybe you know, wish

**[06:45:24]** it was more consensus just means that our field is still immature. We're still looking for those productive ideas. So so that's why I feel like, oh, yes. Not so bad. I think there's some chaos. I wish the field I wish the industry side of the field were going a little slower maybe. So that, you know, we don't have so much know, sort of changing changing landscape underneath our feet. But I think it's also kind of a blessing that it's going to quickly. It makes it

**[06:45:47]** exciting and it's interesting. There's always a new interesting question. To ask. So Yeah. Yeah. I don't have much yet. I'm also quite happy. Actually. Maybe the I mean, the only thing that I'm as, you know, with my students, slightly less happy about is is this timeline, this cycle of every three months. Right? This is a bit of a problem. It has an advantage because if it's not these three months, then you tell them, you know, the idea

**[06:46:11]** is not ready there's the next conference is coming in another three months. And also the workshop system is fantastic. I tend to come now for these workshops more than I come from. The main I I feel there is some sort of self organization happening, what is maybe annoying still is indeed that as I mentioned the failures are not documented. Enough. Right? Because we are benchmarks and driven, We

**[06:46:34]** keep rediscovering a lot of failures, and then I talk to colleague and they say, yes. Also failed on trying to do this. And then I say, why didn't you write this down? And they said, it's not so popular. Right? And it's like doomed to be rejected. So this maybe we should think about, like, graveyard that is visible. Of these ideas that are false or things that didn't try. Right? This is maybe the one

**[06:46:58]** thing we miss. To be Twitter. Well, I really have nothing much to add. Maybe when it's more question about where publications are going since with AI, we can write many I mean, the number of papers written is is becoming huge. Maybe it's about, you know, the the time it takes to actually read some of them that's going to be bottleneck. And, it's I I guess at least you see some companies

**[06:47:27]** may be even not you know, going into peer review, but have rather having blogs. And and for them, it works visibility. But if we go in that direction, then, I mean, the there's a huge advantage of being known already, and it's not really fair. So so how do we maintain, the publication? Is it it going to work

**[06:47:49]** long term or that's more a question. Yeah. I'm not sure if I have any good ideas for Okay. Yeah. Yeah. I I will say one, I mean, one complaint that a lot one one like problem that a lot of maybe scientific deep learning people have like, run into It's like the the conference system like conference reviewers don't always love science of deep learning. Papers. Like, often, like,

**[06:48:14]** a lot of, the ML like, researcher community sort of like a popular opinion is like like I was saying in my talk this morning. There's like two kinds of papers. There's like theory papers which like prove theorems and are about understanding, and then there are empirical papers, get soda. And like don't bother about understanding But like those are the only two buckets it's permissible to be in. And so if

**[06:48:38]** you're in that's sort of I think a viewpoint that exists. In the field. And so I think if you're you're paper is not in one of those buckets, it can be like a lot of people have found it difficult a little bit. With our reviewers, but I I don't think there's a fixed Yeah. May maybe just another, theorists should stick to their guns sort of for that one. You know. Do what they think matters. Yeah. Okay. So this

**[06:49:01]** next question is is it just really inspired by the by the diversity of research agendas know, on display in the talks today. So, you know, you you guys, you know, between you represent, like, just in your talks, interpretability, reasoning, like, self self learning auto generation. It's like scaling laws and data models and and optimization. And, something about

**[06:49:26]** something I think about, I'm curious to hear from you guys is, these are these gonna link together Like, is the is the plan you know, I I when you look at a mature discipline of science, usually it it has a sort of like unified feel or a comprehensive to it or something like that. And so I I wonder how you guys think about this. You know, as you look forward, you think, okay, I'm

**[06:49:49]** in my little pocket, but eventually, it's gonna branch out and connect to the others, you know, like, we'll connect to the edge of stability with neural scaling laws You know, what what's the end goal here? Is that something we should be working towards now or not worried about till later? What do you think? Think? That's good. Let's start with Dave. Alright. Let's start with Rich. I mean, it it should,

**[06:50:16]** You would hope, right, that there would be some TOE right, theory of everything that, but that I mean, if if you look in, there are many scientific fields where they've been working more than a hundred years and they've you know, they're only part way. Right? So I think it's certainly something to aspire towards, but

**[06:50:39]** it it's not just around the corner. I don't quite know what to add. I think they're not as desperate as you think. I mean, I'm sure, you know, you don't wanna be nailed to just interpretability. I'm sure you have done other things. These things are actually more connected. Like, now I work in reasoning. I have a paper in interpretability, for instance, and there, we just knocked out the reasoning piece of the neural net.

**[06:51:07]** Fantastic. Became two lead them. So I'm saying there is connections between these fields, and I we are all traveling along these various patterns, like, big it's like a big field, and you just grace. I I quite happy. Yeah. No. I I think that's that's right. I don't know if I have a piffy piece of advice. I'll I'll help for a minute. Other people. To think about what

**[06:51:31]** they're their answer would be. I think that you know, my my my my emphasis is on gathering this empirical view of what the structures is, this interpretability. And but it's I've always thought of it as a prequel. To understanding what the fundamental structures

**[06:51:57]** are. But it's but I think of it as this round through the field with a certain type of humility. Like, how do we know what theorem we would even suggest? If we haven't walked around the town to understand the landscape is. What kind of things are in this town, what what what detail.

**[06:52:20]** Think that it it it sometimes it feels a little presumptuous. When a first year PhD student comes and says, well, you know, I think that this is the way learning works. And and they haven't really looked around to see what kinds of things are learned. So I think I think that, you know, interpret ability is, least the way I see it, is is a way of building

**[06:52:43]** intuition. That that might empower you to to to, you know, raise theories in the future? Least that's my hope. So I think somehow this question relates to framework that UNIF different ideas, and and framework will always be limited. So, like, I can give a very subjective answer into in terms of how do we think about

**[06:53:09]** building a framework where in my talk, we thought about scaling laws, but in fact, we related it to the emergence of sort of variable. That people see in in NLMs. And I and real have much more complex how they encode syntax and so so the way we are trying to do that is to, you know, how they encode syntax and so on. So the way we're trying to do that is to, you know, develop models of synthetic languages that are actually richer

**[06:53:31]** and richer So how rich should you go? It depends on the question you're asking. And and what you're interested in. So so I think that certainly makes connection between already getting low and in top ability, but I think with everybody, really, because if you think about dynamics, we will we understand the dynamics of deep nets in in general, it will be extremely hard. In

**[06:53:53]** physics, often, we don't understand things in general. So if you think about magnet transition, you know, we we do understand globally all the magnets. We started with the icing model and then it took thirty years to develop, you know, a group, that show that you could classify that many models will behave the same. So I think we're not I mean, my my take is I mean, my strategy that we're not yet there

**[06:54:17]** are the sort of unification. First, we have to understand simple example and when are they useful? What are useful if they make a non fuel prediction that you can then go and test. And so so in this framework, for example, if you think about dynamics for general data, it's would be very hard. But if you have very simple synthetic models of say, yaki. Data, can we understand That's what yeah.

**[06:54:40]** We're some organizer. We're working on 500. So I think that that all way to try to be different. Yeah. I don't have much to add, but I yeah. I I think that everything will hope hopefully ultimately Yeah. I don't know much to add, but I Yeah. I I think that everything will hopefully ultimately Yeah. I don't know much to add, but I Yeah. I I think that everything will hopefully ultimately Yeah. I think that everything will connect. But, yeah, I think for now, it's sufficient I mean, I think sufficient to just work on one direction but, like, be aware of, like, be literate, like, reading and keeping up with other directions

**[06:55:01]** just to like look at connection. Yeah. That makes sense. This will be the last question. It before floor to audience questions. So, if you if you have had if you got a question growing in your noggin, you can line up behind the the microphone. So, yeah, the last question is, what what open question or direction

**[06:55:24]** are you most excited about? You know, like, what what what are you obsessed with solving if it if, if someone told you you know, you can only you can only solve one, you know, you only answer one question or, like, a satisfying answer to one open direction in the rest of your career, like, what what would it be? What would you want it to be? What's the

**[06:55:49]** yeah. Not at all inspired by by AI. Getting really good at science or Mhmm. Oh, and let's start with Jeremy. So I guess yeah. It's hard to depends how I interpret question because there's like there's the biggest open problems like the field. But then there's, like, when I'm gonna work. I don't know how to so I'm

**[06:56:15]** not gonna work on them. Yeah. Yeah. What I'm just taking work on. I'll us the big open problem. Yeah. Yeah. I'd say, like, what is feature learn? Like, everybody knows that neural nets look work because features. Everybody knows that. Like, in CNNs, you have the little Gauss fielders. And, like, in deep nets, like, people have been doing it. Presser ball been doing, like, Meghan Turk. What what is the what is the precise definition of feature and what is how should we what is

**[06:56:38]** the general way in which to reason about that quantitatively? Like, no one I haven't seen any good answers. I'm not working on it currently because I don't have any ideas, but, like, that's the in my opinion, like, the one of the maybe the biggest open problem. Yes. So I don't want to answer in terms of 20 I mean, like, your entire carrier because it I mean, tends to to

**[06:57:02]** change. Yeah. My my period my period is is some shorter even though I think the questions that now we have new tools to address as as was discussed before, like, how language is encoded by machines, how does it lead to reasoning, what's the connection with the brain? I think, yeah, I I I think I could spend twenty hours doing that. I I find it really fascinating. So

**[06:57:24]** maybe the more five or five years question that I think it's, again, relates to interpretability, but also with the you know, so okay. LLMs works great, but then it 10.5 data more than, than our brand does. And so also it seems very stupid to make prediction that the token space Instead, you should be predicting maybe the next idea,

**[06:57:48]** And so, and so you know, is it that the brain also works? So so there is a literature in ML, you know, learning from your own latent, like data to work and so on. But there's actually almost zero theory, I would say. And, and I think it's a fantastic field because it's makes sense also that our brain is not breaking the nice syllables that we're

**[06:58:12]** saying. I see it as another, application of interpretability because if we understand better what's being encoded by latent, maybe we can make machines that are you know, trying to predict their own latent in a better way. That also where I think synthetic languages can help. So I think, this is one. Something that's I think, very rich and

**[06:58:34]** some aspect of it are essentially not studied. Super neat. I I wanna do what you're doing. Not what I'm doing. I I think the fee feature learning is extremely important. I I To me, it's basically taking taking any task that deep where deep learning works and just the simple question of like, how how does it actually

**[06:59:02]** do that? How does it implement right, the the functions that are needed in order to accomplish that task? And then how were how were the how were those functions actually learned from the data? I mean, that's a really like, the low level question is really what what, continues to excite me. Yeah. Thanks. What's the question?

**[06:59:25]** If we had one question, what would be? Or if it Yeah. Like, the biggest open direction. Okay. But you most excited about? I don't reach yeah. Okay. Mean, the question is very, scarily formulated. Right? But nonetheless, I think what I really want to know, and I think we we are all I'm working on the question. Right? Is what is intelligence? And is this deep learning, is that really

**[06:59:47]** the answer to is intelligence? And can it really do what our brains can do? And maybe our brains are not what is intelligence. Right? So for me, this is it's in and and the brain does look different from a transformer. Right? It's does, in terms of energy, in terms of size, in terms of so so for me, it's it's this question of what is intelligence, and is this thing that we have built is it already intelligence, and what's

**[07:00:08]** missing, and this kind of and whatever comes from these questions. Yeah. I I I have a paper that is not from my lab that I tell all my students to read, and I guess maybe that's maybe that represents the problem that I think if I only could work on one problem. That's that's what we should do. And and the question is, you

**[07:00:35]** know, it's related it's it's a reason I chose the subject of the talk if you were at the AM talk. And the question is, you know, how do we learn as humans things that are AIs know that we don't know. Right? Like, because these systems are just they're It's just crazy that that we're

**[07:00:58]** living in. They're so productive. They seem to know they learn features, they learn algorithms, and and some of those are likely undoubtedly, beyond the edge of of like sort of current human understanding. And and I and it just and it's just very puzzling how

**[07:01:22]** to actually learn some knowledge, learn something substantial, learn an algorithm that you had no idea existed beforehand. And so the paper, I I I tell everybody read Lisa Schott's PhD thesis. She graduated a year and a half ago, two years ago, at t.

**[07:01:47]** She worked with some deep line folks to do this for alpha zero chess. To to learn what they these things know that are beyond all chess knowledge use. A professional chess player herself And and they ended up extracting a few pieces of knowledge and teaching it grandmasters.

**[07:02:10]** I don't know how you would do it in anything other than chess. But I I I think it's very I think that the reason I mentioned it is because I think that this might be a problem that we wrestle with as human as our systems get big. There might be an actual practical problem. Of of, like, where we as we learn to live with AI systems

**[07:02:34]** that are smarter than us, how how do we how do we maintain our humanity? How do we maintain our agents feel like part of that is is cracking the puzzle of do we learn what the AI systems know that we don't yet know. Know. Terrific answers. Those were all really inspiring. Thanks. Alright. So we're gonna, the

**[07:02:56]** mic over to to that mic. In order to get through more people, the rules of this will be when you ask your question, direct it towards one of the panelists. That panelist will answer. If anyone else wants to wants to make add some extra comments, you you know, you guys are you guys are free to do that. But, I I wanna make sure we get through a lot of the questions. So

**[07:03:21]** how about it? Hello. Thank you for the panel. So I guess I'll ask you to professor Campe. I wanna see so you mentioned, the thing that difference between like theory and I guess like science. I kinda wanted to ask about as, like, maybe, like, other up and coming researchers, might also feel in a similar manner. Maybe there's like a difference between doing science, on

**[07:03:45]** the models and then, you know, perhaps along with that pushing the intelligence frontier. But, you know, perhaps we want to push the intelligence frontier and we think the best way to do that is a scientific approach. To the research that we're doing. Right? Right? Like maybe like a brute search. We can do a bit more principal search over all the research that we can do. I was wondering whether this is something that you agree with, disagree with, what do you think about

**[07:04:08]** this? And, like, how we can think about doing research to essentially push the frontier of reasoning and intelligence that can be done on silicon. With a percival scientific approach. That was a long question. Yeah. Thanks for the question. So let me try to distill your question first so. Put it in my words. So so you're

**[07:04:33]** asking what scientific principles or methods would allow us to push the frontier of intelligences. Is is that roughly your question? Yes. Like, how can we take a scientific approach to specifically push to frontier and, like, you know, think about reasoning and, know, how we can get that better on silicon. Yeah. So I mean, I can only give examples for this, but, I mean, step one is right? This question is too abstract.

**[07:04:57]** You saw my face. I was already Right? So I would try to find a piece of, you know, of this phenomenon First, you know, don't define intelligence, maybe define you know, put something in the data and ask can I construct a way a machine harness or something to transcend what I just put into my training data? Right? So make it controllable, by controlling

**[07:05:18]** all the variables that matter, design some sort of toy, but not too toy experiment, and then or or theory, and then you know, push the button, execute, and see what happens. Right? And then reformulate your question and and so on and so forth. So I'm not sure this is a very satisfactory answer, but I would not go about asking what is intelligence, how do I push it, I would just narrow it

**[07:05:41]** down to some that my methods or my thinking can solve. Okay. Thank you. Hello. I'd like to address this question to whoever feels most inspired to answer. There was a question, for you all earlier about what should the ultimate goal of a science of deep learning be And I heard most

**[07:06:10]** of you say something like, it should be to enable practitioners. But for me, that seems like it's just begging the question of, like, well, why would we want that? And I would think, actually, we want probably something like a flufy, or something. But then I don't know. It's something like more like you were saying at the end felt more like the purpose. And maybe it was, something, if I could put it in my own words, something

**[07:06:35]** like a science of the philosophy that we care about, understanding ourselves, and also maybe the things we're building. Maybe we don't wanna build everything. And we can understand the optionality of what we build. So I'm wondering, if you agree with me, and if not, why? I'll take I'll take it. I I agree with you. I, you know, I I think that, you know, we have this

**[07:07:02]** dilemma that we are have have designed these systems that work better then we know why they should. Which is a very weird situation for an engineer. It's not something like that. I don't know. I was computer systems don't work. Know, why I still can't get my printer to work you know. You know, I I I don't know why it is.

**[07:07:24]** That I, you know, I train a deep learning system and it works better. Than I thought it should. Why why it can solve problems that I couldn't solve. Right? Like, how how does how does this happen? And and I and I so I do think that because of this, we're confronted with this question of how do we maintain agency, and intuitively, it feels like understanding the systems better

**[07:07:48]** is part of that, and I think that's why. I think that's one of the drivers behind the need to understand the systems better. Hello. I'm gonna direct my question. I used to Jeremy. Mostly written by virtue of not being David to has already answered this question. For a lot of people, when I talk to them about, like, science and deep learning stuff, they often express confusion or uncertainty about,

**[07:08:17]** like, how to go about doing high quality work. And so I was wondering if you had, some examples of work that you can serve particularly high quality. You'd recommend people look at and kind of like, model work that they do off of especially work from outside like you and your collaborators, because because just out of curiosity. Yeah. No. It's definitely hard to I mean, yeah. It's definitely hard

**[07:08:41]** I find it I find it hard to do. Work in this field. Yeah. I'm trying to think Like, I know there are a lot of promising are a lot of direct, like, like part of like you should you should read the the, position paper that Jamie

**[07:09:12]** and others have recently put out there will be a scientific theory of deep learning, which has a lot of good leads. But, yeah, I I find it very hard to yeah, and also just to, like, Yeah. It's definitely hard. No no specific, like, mind? Let me see. I mean, like, what makes science of deep learn? Like,

**[07:09:45]** Yeah. I mean, like the the mute p like the there's like good works around MUP and related areas that are very interesting. Like, for example, like the, you know, the Jeremy Bernstein line of work. There are I don't know. I see lots of papers every, like, every month that I find I find at least fascinating. I I haven't dived

**[07:10:23]** deep I haven't gotten a chance to dive deep into many so I'm not sure which I would I don't have a reading list. Pre prepared reading list. Other than the one in in the the, position paper. Okay. Thank you. Oh, Dhruv Dhruv's paper is actually very on on a I would point to Dhruvah's

**[07:10:47]** paper. On, Word2vec. Actually. Thank you. Thanks for all your help. Which is also getting at the question that I understanding, like, why, linear analogies work in word two vec. Alright. So due to time constraints, this will be our last question. Yeah. Sorry. Sorry, Caden. You guys can rock, paper, scissors for it if you want.

**[07:11:14]** Thanks for the really cool panel. I just had a question actually about a answer that David gave earlier. About, how one hallmark of really strong science is that it serves as conceptual scaffolding for future insights or future projects or stuff like this. And maybe this is a skill issue on my part, but I only see the scaffolding after I've done a project, and I wanna know if there are any concrete heuristics during

**[07:11:37]** the problem selection phase that I should be know, trying to to to steer my interest towards something that a future project could build on. Assuming that things work out and stuff like that. I don't know. Maybe I can give an example again Sure. By example thinking, and maybe then also, I don't know. Maybe I can give an example again by example thinking, and maybe then also, could be interpreted as an answer. Jeremy, could have given. So in our perspective, we can look what papers actually

**[07:12:04]** had a lot of impact. That came from with a scientific Sometimes it was the papers that asked the question, and I'm thinking now of one which is a very old paper. I think it was, what, 02/1718, So what memory no. Learning requires sorry. Understanding deep learning requires understanding memorization. Where they designed this where they just mixed up all the labels, had

**[07:12:27]** the training set with this, and lo and behold, it the thing had, like, zero training wheels. Right? Simple. Right? Afterwards. Beautiful question. Tons of follow-up work. I mean, people zag it all, I think. Still cited. I don't know how many years later, but that's in impact. Right? That's about asking questions. So I think these kind of things are setting the stage also for lot of there

**[07:12:49]** are many more such works. Right? In context learning work where then there was this thing, oh, it's like doing some sort of meta gradient descent on the in context example It's a whole line of works, not a I think in retrospect, we can answer this question. Going forward, I would if I could, I would just write. The next paper. Right? So it's a bit Thank you. Yeah. But it sounds like your suggestion is simplicity.

**[07:13:12]** Right? That sometimes right, so sometimes it's not it's not the first paper to do something. People have been digging around an area and sometimes there's a paper that says, oh, look at where we're all digging. Oh, here's a simple way of looking at it. And then that's and then that that becomes It becomes accessible to people. They now now people have a framework for understanding what to think about, and I think that maybe that's

**[07:13:34]** phenomena you're talking about. Right? That could be a thing to do. So you don't so yes. So don't don't necessarily so I I I so I usually tell my students to that the way to be risk averse is to be creative. It's to, like, go do something that nobody has done, like, everybody else is afraid of. Something new. And

**[07:13:59]** I usually tell them be very careful about working in a busy area that a lot of people are in, because it's it's harder. To do good work. But on the other hand, if you wanna do something really productive sometimes, it it is to look in a busy area and then think about how to simplify it. And that could be very impactful. People will be interested in that. So yeah.

**[07:14:23]** Thanks. That was really useful. Alright. Thanks so much. Everyone, let's give them a hand. There's, there's one more t shirt if anyone wants to. Although, I think it's a small. But yeah. Okay. So the the next thing will be, Sara will be telling us about, winners of our challenge. Alright. Okay. Thank you. Thank

**[07:14:54]** you all the panelists, and thank you everybody for sticking around till the end of today. So the last talk is going to be in line with the first question and answers that we got here, actionable science. Right? So the challenge of the workshop this year was how can we use our understanding, our scientific understanding of AI to improve our models.

**[07:15:18]** How can we them in practice, put this understanding practice? The winner this year was paper submitted on the induction bias in sequence models and, we're gonna have Reza Ibrahimi, he's an assistant professor, in no. There's a change of plan. Okay.

**[07:15:47]** Okay. A change of plans. Roland, Miseveil, Miss Servic. Was that right? Close enough. Yes. Okay. You very much. So Okay. I think this should work. Well, thank you very much to the organizers of this workshop for this very nice workshop, and thank you also for

**[07:17:00]** giving us this, very nice award for, our submission. My name is Roland Mimisiewicz. I am one of the coauthors on this paper, Ibrahimi, the first author on that paper unfortunately couldn't travel. To to ICU this year. And so I'm going to present this work and, it's a collaboration with the four of us.

**[07:17:26]** So, apologies ahead of time. So I'm going to pour some cold water on, the transformer. AGI. It's around the corner party. I think I think that's kind of what this work is about a little bit. And I'm going to present our work that does this by, very, very, narrowly studying a set of tasks

**[07:17:48]** that test the very specific capability in these models, or the absence of that capability, which is commonly referred to as state tracking. And then, I'm gonna make the case for recurrent nets, as a much better model of, both the ability to do state checking and also, I believe, intelligence of various kinds and especially human like, understandable, reasonable intelligence. So there's

**[07:18:12]** a very well known set of results over the last couple of years that has shown that autoregressive transformers, no matter which breed position embedding variant, whatever you wanna consider, which size, they all are unable to generalize very, very simple state tracking tasks across sequence lengths. So specifically, if you take a task like

**[07:18:36]** parody, where you have a bunch of zeros in once, you go left to right, you count the number of ones, and then you state in the end whether they are odd or even. So you do counting of the ones left to right, module two. It turns out that, if you so if you train that model on a sequence length say, 10 to 20, and then you test it on length 30, the performance sharply drops. And

**[07:18:58]** so what this means is you really have to train them on the length of the sequence that that you wanna test them on later, and so that's true across the board. There's just no transformer model that is able to learn to generalize out of distribution this way. It doesn't change whether you do this directly, so you ask the model to just output the answer to the question, or whether you allow it to do a chain of thought

**[07:19:21]** or synonymously sometimes called scratch pad, where the model goes left to right and creates the running solution along the way. No matter which, it just doesn't generalize out of distribution this way. So So what we wanted to do in this work is to understand whether or not this, inability

**[07:19:45]** is really an out of distribution problem. Or whether it's simply the absence of an appropriate inductive bias, that, lets the model fail. And if it's about the inductive bias, then we would also assume that it's not just an out of distribution problem, but it somehow impacts the performance of a model on this kind of task in distribution. And so the way, classically, in machine learning, we would study this

**[07:20:09]** is by looking at the data efficiency of a model on this kind of task. And so in this study, we take three types of model. Transformer g p d two, all in the single digit millions of parameter range. GPD two six layers just off the shelf kind of what was commonly used in 2019 or something like that. Then we take an LSTM, roughly similar size, but a

**[07:20:32]** single layer in this case, and we take a dense state space model, which is specific kind of recurrent net, the hidden to hidden transitions are full matrix and not a diagonal matrix. But that include that excludes all of the currently popular linear RNN, state space model type models, It's a very specific recurrent net that cannot be parallelized, but turns out to be really, really

**[07:20:56]** good for this kind of task. So And, so the findings in a nutshell are that, data requirements for transformers grow like crazy as you increase sequence lengths. Even in distribution. And, unlike RNNs, transformers don't really learn to decompose this task into a step by step computation, but their performance is really linked

**[07:21:21]** to a particular sequence length. And so as we'll show in a second, training a model on length five or length 10 or length 12, is each time a completely different task for a transformer. Whereas for an iron in it considers all of these sort of the same type of problem. So here's a methodology. So the task in this case is predominantly

**[07:21:44]** modulo addition, so it's a generalization of parity, so you have a bunch of numbers add them up. Modulo. Five, and for example, we consider three supervision regimes. For these models. One is outcome supervision, which, is what you see on the input, you get an equal sign, and then you just have to output the answer. The other one is chain of thought, which I talked to talked about

**[07:22:06]** before in the case of parity. So you run you create the running answer, and then the last element of that will be the the the correct final answer. And then we do another one which we call aligned chain of thought, which works well specifically for RNNs, where we also do chain of thought, but the outputs are generated along the way as you process the sequence. And and, we test these types of models

**[07:22:29]** and and and supervision regimes across three scenarios. We train the models on a fixed sequence, of a fixed length, train them on a whole set of lengths between two and that target length, and we train them in a curriculum from short to long sequences. On that whole set. Of lengths. And then we, so we do that in

**[07:22:51]** in around 200,000 training runs in the end, by doing a binary search to find the optimal or smallest number of training examples, for which each of these models, each of these settings, and so on is able to give us a particular, stopping criterion, which is like 99% or something like that. On validation. So so I what is the minimum of amount of data

**[07:23:14]** you need to really learn this task sufficiently and generalize in distribution? And so here's the master table, I'm gonna show some slices of that in a in a second, there are several take home messages that you can see by just kinda squinting at this. On the top right, you see the outcomes, so the number of training examples you need for the transformer. On the bottom, you see on the left LSTM, on the right, the bilinear

**[07:23:39]** RNN. Slash dense state space models. And so one thing you see is this transformers really need chain of thought. That's the middle row on the top panel there. And they do really really well on the fixed setting. Which is you only do the task on one sequence of one length. Say, a length 10, and that's it. And, you don't need to generalize across

**[07:24:01]** lengths. They do reasonably well also in the uniform setting, that's the middle column, if you give them a chance of thought, supervision, but they need significantly significantly more data, and so that setting is the one where the model has to generalize across all lengths up to the target lengths in this table. And on the very bottom, you see a line chain of

**[07:24:24]** thought for the two RNN type models, and, that's the preferred method. For these models, and, they don't really care that much whether it's fixed multiple sequences, or short to long. They always work, and they only need something like single digit, sometimes 10, 20 training examples to work perfectly on these tasks. So here are some slices to to understand these tables better.

**[07:24:48]** On the top left, you see a comparison between channel sort and aligned chain of thought, a function of sequence lengths, and you see that LSTMs in blue do much better when they get a line chain of thought. The dashed line, and transformers do much better when they get chain of thought. Which is the solid line

**[07:25:10]** on the top right, you see a plot that shows us that RNNs are much much more data efficient in the outcome supervision case. So they can solve the task reasonably well with very few training examples no matter what the sequence length is. For some settings, and, they don't grow much either in terms of data needs, whereas the transformers fail already at

**[07:25:33]** length 10. Plus. On the bottom left, you see a slice that shows that sometimes RNNs longer sequences actually lead to a smaller training set requirement, and that is because if you consider adding numbers together, adding three numbers, adding four numbers, adding five numbers, etcetera, are sort of always the same task. So every step of it gives you some supervision.

**[07:25:57]** Transformer just cannot catch in on that. And, I'm gonna skip over the last one and instead show one more variation that we study here. So we see that transformers kind of do weird things when they have to generalize across multiple sequences. Length sequence lengths. And so to study this a little bit more formally, we do one more thing, which is we,

**[07:26:21]** consider a setting where we have a system like like a mixture of experts, if you will. You take a sequence, you depending on the sequence length, you route that sequence to a model was only trained for that one sequence. So you get a sequence of length seven, you take the length seven's transformer. Then you get a sequence of length nine, you take the length nine transformer. This end, you have to train one model for each sequence lengths.

**[07:26:44]** And the amount of training data you need to do that system to train the system well is gonna be the sum in the numerator. Of that quantity over there. And we compare that to a model that is trained across all sequence lengths at once. Any reasonable model, you would assume, is going to do better when it's trained to course all sequences at once, because these sequences are fundamentally identical to another. It's

**[07:27:05]** just different sequence lengths. But that's not what you see for transformers. So in the chain of thought supervision regime, which is in the middle, the very left plot in the middle, you see that the amount of data as a function of sequence length in this experiment grows significantly faster if you have a single shared model than if you have an independent model. And the exact opposite is true for the

**[07:27:30]** LST LSTM. So the preferred method there is aligned chain of thought, which is this one. And you see that the single shared model basically is the multiple independent models just accumulate more and more data because there are multiple different models. Anyway. And we can quantify this. This is sharing factor Kappa and you see that RNNs have a very high sharing factor and

**[07:27:54]** factor. And since I'm running out of time, we did this across a whole bunch of tasks, not just module addition. But I'm gonna conclude in the interest of time, so I think from these experiments and similar things that people have been showing lately, the community one conclusion a speculative conclusion perhaps that we can draw from this is, in your interest of scaling, the community

**[07:28:18]** has sort of abandoned a very, very, very natural inductive which of the elements in a C And, that makes them scale well, you can train parallel and so on, but the flip side of that is, they also need scale. So, even for something like adding a bunch of numbers from zero to 10 together for a given sequence length, you need outrageous amounts of training

**[07:28:43]** data to to convey that concept. To the model. And, so that's a very very strange thing that's just due to the absence of that bias that humans evidently, have, which is true step by step processing one one digit at a time, one one token at a time. Recurrent nets are a very appealing alternative. They have other dish issues. They cannot be trained in parallel on giant training sets and

**[07:29:06]** so on. And generally, it it raises questions of where is this all gonna go? And, so speculatively, what I would assume is memory augmented RNNs, or hybrid models where the attention is really, really, really short, so it can't allow the model to learn shortcuts and cheat its way

**[07:29:28]** to to a solution on the training data might be ways. This can unfold. But are really early in this, it's not transformer, don't really know what it's gonna be. And we'll have to see for the next few years or decades of where this can all go. So I'm gonna finish here. I think I'm way over time. Thank you again for this award. And, thank you for listening. Thank you very much.

**[07:30:00]** Because we are running a bit over time, let's so there's gonna be a poster session and let's ask questions during the poster session, if you are sitting around for that. I'm just gonna say a few words is the first poster is a challenge, winner poster. If you're gonna go to that, I'm gonna say a few words to close

**[07:30:23]** the workshop. So let's see if I All four sticking around on the lam. Maybe we can't close the workshop. Stop marrying. So Let's play in Alright. Good 24, add more reps.

**[07:33:10]** Hopefully, there's gonna be more iterations. So our goal for launching this workshop in the first place was to turn the science of deep learning into its own subfield. And it feels like it's been already a a bit effective. At least I see more people who describe their research as like science of deep learning, more and more, and maybe

**[07:33:34]** we can take some credit for that. We can, a very small portion. And but like Rich said during the panel, this is still a very small community. Out of all the people who come to who come to these major ML conferences, only a small percentage are interested in understanding deep nets in a scientific way.

**[07:33:59]** But, yeah. So so most of the time, we encounter this question that, like, why why do we even need this? Science of deep learning? It's a really rich landscape, and there is a lot of so between theory and practice, we do need a bridge, and, there's a lot of fun and interesting questions that lie in this

**[07:34:22]** in between of these two extremes. And hopefully, this workshop is one little step in getting closer to unveil these mysteries about deep nets. And as we saw today, and it was featured in the workshop, it's an interdisciplinary risk, effort, Really, we need, like, all of these different perspectives from, like, signal processing

**[07:34:48]** to to physics, psychology, neuroscience, all of these people who thought about deep nets. To, bring their expertise and approach it together. Yeah. So I just wanted to thank my, co organizers, Thank you a lot, speakers, contributor speakers, and all all of you who submitted papers, to the workshop. And, hope to

**[07:35:12]** see you all in the future iterations. Thank you. And there's a poster session until it runs until five.
