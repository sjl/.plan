This is my personal notebook where I dump thoughts and notes for my future self.

**I make no guarantees about the accuracy of anything in here.  Read at your own
risk!**

[TOC]

# October 2023

## 2023-10-01

Put up a bunch of stuff for sale on the PIBS list.  Need to declutter my
apartment now that I've mostly moved in.

Did a few hours of work on Lab 1 for BS521.  Too much unproductive screwing
around in R trying to figure out how to get decent fonts.  Should be able to
finish it up tomorrow though.  Random notes jotted down from the process follow.

Side-by-side figures in LaTeX:

    \begin{figure}[h]
        \begin{minipage}[t]{0.48\textwidth}
            \includegraphics[width=\linewidth]{figures/bp-histogram}
            \caption{Distribution of blood pressure among participants.}
            \label{fig:bp-histogram}
        \end{minipage}
        \hfill
        \begin{minipage}[t]{0.48\textwidth}
            \includegraphics[width=\linewidth]{figures/bp-nqq}
            \caption{Normal QQ plot of blood pressure values.}
            \label{fig:bp-nqq}
        \end{minipage}
    \end{figure}


Reasonable quantile plot in R:

    qplot <- function(filename, data, label, main, ...) {
        n = length(data)
        plot(((1:n - 1)/(n - 1)), sort(data),
             type = "l",
             main = main,
             xlab = "Quantile",
             ylab = label,
             ...)
    }

QQ plot with the damn line in R:

    nqqplot <- function(data, ...) {
        qqnorm(data, ...)
        qqline(data)
    }

Reading in a CSV with specific column types:

    data <- read_csv("EPID_521_lab_data.csv", col_types="iddfiffdffdd")

Note that this seems to give you a "tibble", whatever the hell that is.  Some
kind of tidyverse thing?  It's very confusing that everywhere you look there's
a hairball of a mess of base R, tidyverse, and ggplot2 and everyone just assumes
you understand which is part of what.

Reordering levels:

    data <- mutate(data, diet=factor(data$diet, levels=c("Poor", "Fair", "Good", "VeryGood", "Excellent")))


Removing rows with `NA`s for e.g. the `cot` column:

    data <- data[complete.cases(data$cot),]

Histograms with specific bin widths, rather than a number of bins:

    hist(data$age, breaks=seq(from=15, to=90, by=1), main="", xlab="Age")

Multiple box plots in one image:

    boxplot(bmi~sex, data=data)

Marking and/or filtering on a boolean condition:

    data$locot <- data$cot <= 0.011
    locot <- subset(data, cot <= 0.011)
    hicot <- subset(data, cot > 0.011)

## 2023-10-02

HG545 review this morning.  Need to go back and review the first module again
tomorrow since it's been a while.

Finish BS521 lab 1, finally.  That was a lot more work than I expected.

Met with a professor about possible rotation.  Need to chat with my advisor to
see if there's special paperwork I'll need.

## 2023-10-03

BS521.  Confidence intervals.

BI500.  Research writing.

Finally got around to splitting my Vimrc into minimal and extra files, so I can
sync the minimal one to servers and not hate myself when trying to edit. There's
some jank involved around the colorschemes and `set termguicolors` but I think
have have something that should work.

PIBS800.  Mentor/mentee relationships.

## 2023-10-04

Advising meeting.  Need to do a couple of things in EdM and register for 602,
but I'm currently blocked on both by other folks so I'm good for now.

HG545 exam.

## 2023-10-05

Finished the HG545 exam last night.  That was… deeply unpleasant.

BS521.  Hypothesis testing.

BS521 reading.

Read the paper for HG545.  I get the general idea, and it seems like a pretty
clear experiment.  I wonder how much we'll stick to the paper vs going off topic
this time.

Needed to convert some PDF graphs to PNG to put in a presentation, but `convert`
was whining about some security crap:

    ><((°> convert n50.pdf n50.png
    convert-im6.q16: attempt to perform an operation not allowed by the security policy `PDF' @ error/constitute.c/IsCoderAuthorized/421.

Turns out there was a bug in ghostscript, which was fixed, but convert still
doesn't trust it so won't convert stuff.  Great.  Have to edit
`/etc/ImageMagick-6/policy.xml` and comment out these lines to make it behave:

    <!-- disable ghostscript format types -->
    <policy domain="coder" rights="none" pattern="PS" />
    <policy domain="coder" rights="none" pattern="PS2" />
    <policy domain="coder" rights="none" pattern="PS3" />
    <policy domain="coder" rights="none" pattern="EPS" />
    <policy domain="coder" rights="none" pattern="PDF" />
    <policy domain="coder" rights="none" pattern="XPS" />

Skimmed through the slides for HG545 tomorrow.  It's nice to be able to get
a preview of things again.

## 2023-10-06

HG545, class was about splicing.  I feel much better about this module thanks to
being able to prepare a bit with the preview last night.

## 2023-10-07

Installed <https://github.com/numcommand/num> — might come in handy here and
there.

## 2023-10-08

Reread the paper for HG545.  It's… a little clearer now?  Though honestly it
wasn't too bad before compared to the other papers.  Just a lot of acronyms.
Got a list of things to ask.

## 2023-10-09

HG545 this morning, about co/post-transcriptional modification.  The downside of
having slides is that people put a ton of things on them and you can't take
notes fast enough.  Need to go back over the slides and write down things once
I get home so I don't forget them.

## 2023-10-10

BS521, hypothesis testing, p values, t distribution.

BI500, code quality tips.  Checked with Prof. Sartor and submitting a LaTeX PDF
for the references homework is fine.

Pinged a few students in a lab I'm interested in to see if they're willing to
chat about their experience.  Just need to nail down my third rotation and then
I'll be all set.

Ordered a used copy of the Grammar of Graphics book.  I've read enough in the
ebook copy from the library that I know I want the entire thing, even though
it's quite expensive.

Read chapter 4 of the book while the straggler genomes finish in the last batch,
about variables and basic transformations on them.  The book uses the ridiculous
terms "homoscedasticity" and "heteroscedasticity" to mean "homogeneous variance"
and "heterogeneous variance", which I *think* is the same idea as Cleveland's
"monotone spread" (or possibly a more general version of it).

I really wish the book wouldn't omit the axis-drawing code from the diagrams
— it makes it unclear where each piece of the output is coming from.  I think
I *mostly* understand it, but would prefer if it were all explicit (even if it
would make things a bit longer).

Read chapter 5 too, on algebras.  This was much, much more confusing and would
have been much clearer with more explicit examples.  Need to read this at least
one more time to get it, I'm sure.

Going back to take some notes for HG545 while they're still (vaguely) fresh in
my mind.  First: notes from the class on splicing.

The "R-loop" terminology is confusing.  It's inspired by the name "D-loop",
which notes how DNA will unzip to show a loop when it's being duplicated (and
there's a complementary strand bound to one side).  "R-loop" *also* refers to
the loop *in the DNA* when it's bound *to RNA* (e.g. when it's being
transcribed).  Again: the actual loop in an "R-loop" is a loop of DNA.

An RNA molecule has 3 relevant sites when considering splicing:

```
 5' exon |                  intron                            | 3' exon
 ======AG|GUAAGU============================YNYURAY====Y₁₁NCAG|G==============
                                                 ↑
      5' Splice Site                    Branch Site      3' Splice Site
```

Note that in this case the branch site is specifically an adenine.  That's
important (reason comes later).

One important aspect of RNA that allows it to be spliced (contrasted with DNA)
is the hydroxyl group on the 2' carbon in RNA, which is not present in DNA
(that's why it's *deoxy*ribose).  That hydroxyl group is what attacks the
phosphate bond at the 5' splice site and cleaves it apart (after being brought
close to it by the spliceosome).  That leaves a hydroxyl group exposed hanging
off of the 5' exon, and in the next step *that* group is brought close to the 3'
splice site and attacks it.  Once that bond is broken the intron (as
a lariat-shaped thing) floats away, and the exons are spliced together.

The chemistry of the breaks is called "transesterification": two
phosphodi*ester* bonds are broken (at intron/exon and exon/intron boundaries),
and two more are created (one in the lariat, and the splice between exons).

(Of course like everything in biology, in reality it's all a giant mess and there
are multiple kinds of splicing, including self-splicing.)

The spliceosome is a giant thing made of a bunch of different proteins and also
5 RNAs that mediates splicing.  The RNAs are important because those are what
recognize the splice and branch sites through complementary pairing, e.g. at the
5' splice site we have:

       ____________
      /     U1     \  U1 component of spliceosome
      \            /
       \__CAUUCA__/
          ┆┆┆┆┆┆
        ==GUAAGU==    RNA

In a similar way, the U2 component binds to the branch site, but the binding
sequence specifically skips the adenine at the site, which "extrudes" it from
the RNA a little bit:

              extruded adenine
                   ↓
                   A
    ======U A C U A C=======    RNA
          ┆ ┆ ┆ ┆ ┆ ┆
       .——C A U U C A——.
      /                 \
     /        U2         \      U2 component of spliceosome
     \___________________/

Alternate splicing is also a big deal, because it allows the creation of many
different mRNAs from the same gene by bringing together different exon/intron
boundaries to be spliced instead of always splicing the closest one.

Of course there's other complications too, like splicing enhancers and silencers
that can recruit/block the splicing machinery.

Skimmed over tomorrow's HG545 slides so I don't have to go in blind again. Seems
pretty reasonable, though the end seems pretty rushed and I *think* it's
relevant to one of the questions in the homework.  Need to pay attention at the
end.

PIBS800, how to read a research paper.  I feel like I've had three versions of
this presentation by different people at different times at this point.

Started BS521 homework 5.  A bit more confusing than the previous homeworks, and
it's been a week or so since I touched LaTeX so I once again have to fight it
every step of the way.

## 2023-10-11

HG545 this morning, about translation.

VA onboarding after that.  Took a couple of hours, but I now finally have
a badge.

Been reading the GoG book during some spare free minutes here and there.
Skimming over a lot of the formalism, I still feel like this could be much
improved by showing some full examples with everything laid out.

Sketched out some answers to HG545 questions.

Finished BS521 homework 5, turned it in.

Cleaned up HG545 answers.  Need to do one final pass tomorrow.

## 2023-10-12

BS521, started talking about two-distribution t tests.

Finally got around to swapping my search engine on my phone to Kagi.  The
degoogling continues.

I really need to figure out a decent way to do proper pivot tables in Postgres.
From reading the docs it looks *surprisingly* janky for what I'd expect from
Postgres.

Read up on index operator classes, which was preventing Postgres from using an
index when searching for a prefix of a string, e.g. `SELECT name FROM foo WHERE
name LIKE 'pref%';`.  Fixed by telling Postgres this index will be used with
text patterns by e.g. `CREATE INDEX i__foo__name ON foo(name
text_pattern_ops);`.

## 2023-10-13

HG545 discussion.

## 2023-10-14

Fall break.

## 2023-10-15

Did the BIOINF-500 homework on reference management/citation.  Figured out how
to get Latex set up to do references.  Lots of jank, but I think I've got it
working now.  JabRef produces a `.bib` file as its database.  Then in the Latex
document, add a preamble:


    \usepackage[
    backend=biber,
    style=nature,
    sorting=ynt
    ]{biblatex}
    \addbibresource{sjl.bib}

Cite things with `\cite{foo}` and `\cite{bar,baz}`.  Then `\printbibliography`
to put the references section into the paper there.

This is complicated by the fact that you have to run `biber` between runs of
`pdflatex`, so I kludged together a `mklatex` script that does something
horrifying like `pdflatex; biber; pdflatex; pdflatex`  to actually make the damn
document.  Gross.

I really need to get my latex stuff into a set of files, rather than
copy/pasting everything into every single document.

## 2023-10-18

Back from fall break. Time to get back into the swing of classes.

HG545 this morning, starting the section about transposable elements.  The
professor put up slides, videos, and a narrative document in advance which is
really great — I was able to prepare and not be completely lost.

Read over animal ethics stuff for tomorrow.  Need to consider if I want to
really do a rotation with animal subjects.  I'm a little less sure now.

## 2023-10-19

BS521 this morning.  The second half of the class has a different lecturer,
starting today.  Talked about paired t-tests (which are essentially just doing
a one-sample t-test on the difference of the paired values) and ANOVA for
many-sample t-testing.

First PIBS503 discussion section.  This is (I think) the only one that's in
person, and it's in the middle of goddamn nowhere on the North Campus.
I managed to find my way there, but dear god are these buildings confusing.

BISTRO at 4. Topic: HMMSTR, using HMMs for tandem repeat copy number detection
from ONT reads.

Need to remember to ask Alan if he has any suggestions on reading material
I should look at over the weekend before I start with him on Monday.

## 2023-10-20

HG545.  More on transposable elements, this time about LTR retrotransposons.

Met with Bob about rotation paperwork.

Last day of my first rotation!  I think it went well.  Looking forward to trying
out more things in the next few rotations, but this one was great!

## 2023-10-21

Finished reading the HG545 paper, finally.  It was long, but a lot more clear
than the other papers thanks to the supplementary material actually *explaining*
things.  So even though it was a little tedious to get through with so many
abbreviations, I think I preferred it overall to the other papers so far.

Finally got around to hooking up a keyboard shortcut for `switch-yubikeys`
since I find myself actually using it a lot again, now that I'm not working from
home full time.

Sent my lab notebook to the PI, which is my last official act of the rotation.

Swapped out a fresh VM for my next rotation.  Keeping the old one around for
a few weeks in case I end up needing anything from it.  Glad I've got everything
scripted up around this — much easier to do it this time.

Started BS Lab 2.  Not going to do the extra credit this time, I just don't have
the spare time at the moment.  Too much going on all at once.

Installed Weechat+wee-slack and irssi on my laptop.  Going to give irssi a try
for a while as an IRC client, which would let me reserve Weechat (which I don't
really like all that much) for Slack.  Irssi config was a little janky, but
I think I got something dogfoodable for now.

Installed the Python lib for the next rotation on the VM in a venv.

## 2023-10-22

Finish BS lab 2.  Didn't go the extra mile on this one either, still trying to
catch up from break.  I'm getting there though.

Figured out some travel/break logistics for between semesters.

Finished BS homework 7.  I should be all caught up on stuff for that class
(aside from reading, which goes quick) for a while now.  Next big thing for it
is the exam on 11/02.

Got a couple of LaTeX snippets to remember after all the biostat stuff.  First,
often worth making shortcuts for frequently used stuff in a given assignment:

    \def\h0{\textbf{H}_0}
    \def\hA{\textbf{H}_A}
    \def\tstar#1{t^\star_\textit{#1}}

Adding spacing between equation lines with `\jot`:

    \begin{equation*}
    \setlength{\jot}{10pt}
    \begin{split}
        T & = \frac{\bar{X} - \mu_D}{s/\sqrt{n}} \\
          & = \frac{-0.545 - 0}{8.887/\sqrt{200}} \\
          & = \frac{-0.545}{0.6284058} \\
        T & \approx -0.867 \\
    \end{split}
    \end{equation*}

Started HG545 homework, just sketching out notes.  Burned out before getting too
far, will have to actually get a rough draft done tomorrow (then cleaned up on
Tuesday).

## 2023-10-23

HG545, about the L1 transposition assaying and Alu.

First day of the new lab rotation!  Set up `black` on the laptop since I'll be
doing Python.  Ended up installing it into a venv and symlinking to the binary,
which seems to have worked okay.

Need to figure out how to get Irssi to autoload scripts properly and set up
e.g. `/toggle awl_viewer` on startup so I don't have to do it by hand every
time.

Got a first draft of HW5 90% done.  Will finish tomorrow.

Did some reading for BS521.  Still have a little left for Thursday.

## 2023-10-24

BS521 today.  Got another intuitive explanation of ANOVA (which was nice) and
talked about categorical CIs/hypothesis testing.

BI500.  Presentations by faculty who are looking to recruit students:

1. Statistical/online bioinformatics.
2. Cell lineage trees via imaging + ML.  If only there was a way to kludge
   something into mitosis that would tag descendant genomes ala service request
   ID tagging (or even just e.g. a plasmid that would mutate quickly as
   a clock).
3. Head/neck cancer and ALS research via multiomics and large cohort studies.
4. How molecular/biological clocks work.
5. How cell cell signaling controls cell fate in human pluripotent stem cells.
6. Exercise, multiomics, and wearables, cell communications and differential
   expression with ML.
7. Wearable and multiomics data to identify biomarkers for early
   detection/prevention of disease.

Should also look into the additional ones who couldn't be fit into timeslots to
present.

Lunch at Maizie's.

PIBS 800 about grants, e.g.
<https://rackham.umich.edu/funding/rackham-graduate-student-research-grant/>
which can be done as a pre-candidate *and* candidate.  I think I should get Cat
to explain this to me in idiot terms so I can figure out all the stuff I'm
missing.

Met with study group for HG545 homework.  I feel like I understand everything
very well, but trying to fit a coherent explanation into the line limits of the
homework is absolutely miserable.

Finished HG545 homework.  Walking unsteadily as I emerge from the prose-gutting
facility covered in texual viscera and stinking of article blood, my filleting
backspace key dull in its socket.

## 2023-10-25

HG545 discussion this morning.  Chatted about a bunch of stuff, nothing too
groundbreaking.

Spent the rest of the day in the lab.

Put together my new table at home.  Looks nice.

Reviewed the files for the next two 503 discussions this week.  Nothing
really surprising here.

Did the BS521 reading for tomorrow.

## 2023-10-26

BS521 class this morning.

I've got the 503 discussion thing at 2, need to figure out a good place to take
that Zoom call.  Maybe the study rooms at the top of THSL?  Need to figure out
how to reserve those at some point.

PIBS 503 discussion class zoom meeting.

Started reading the next HG545 paper and glanced over the slides.  I wish we had
lectures recorded like the last module.

## 2023-10-27

HG545 lecture.  New module starts today, on replication.

There's more than just one DNA Polymerase.  Three main ones are called α, δ, and
ε.  Roughly, α starts, then hands off to δ.  On the lagging strand, that's all
it has time for before it falls off and the process starts again for the next
Okazaki fragment.  But on the leading strand, δ has time to hand off to ε, which
is much more stable and can continue along the strand.

Proofreading and mismatch repair are both very important.  The initial
polymerization process has an error rate somewhere around 10⁻⁶.  Mismatch repair
happens *in-line* with the replication process: DNA Pol doesn't like continuing
from a mismatch based, so most of the time it will pause for a bit and the
proofreading machinery that's also in the replication complex will chomp off the
bad base, then DNA Pol will continue. Mismatch repair happens separately: one
protein recognizes the mismatch and recruits another protein that excises the
match *and a big chunk of the downstream strand*, and that whole chunk gets
resynthesized.

Another PIBS 503 class discussion zoom meeting.  3 down, 4 to go.

## 2023-10-28

Started digging into the HG545 paper.  I hate that we only have 2 classes for
this one, it feels far too rushed.

## 2023-10-29

Finished the second readthrough of the paper.  I feel a little better now, but
am still not perfectly sure on the questions.

## 2023-10-30

HG545 class, mostly on DNA repair.  Makes the case that a lot of DNA repair
reuses the same polymerases (e.g. δ) as replication (but not all, e.g.
single-base repair uses something else (I think β?)), and you can kind of think
of it as just another form of replication.

Another important point: replication is not deterministic, because it doesn't
have to be.  As long as the whole genome (well, chromosome) gets replicated, it
doesn't matter precisely where that replication started.  This is very different
from e.g. transcription, because starting in a different place would transcribe
a different gene.

Also important to define terms like lesion vs mutation: a lesion is detectable
DNA damage, which then get fixed into place (in the "use fixer on the photo
paper" sense, not the "repair" sense) by subsequent replication.

I think I'm feeling a little better about the homework questions now after
talking through it a bit.  Need to get some rough drafts sketched out for when
I meet with the study group tomorrow.
