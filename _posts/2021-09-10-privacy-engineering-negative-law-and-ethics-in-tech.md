---
title:  "Privacy Engineering, Negative Law, and Ethics in Tech"
date:   2021-09-10 12:13 -0800
categories: analysis
---
This week I started attending a [Transnational Law & Practice intensive](
https://www.law.uw.edu/academics/continuing-education/summer-institute) in
preparation for my Master’s degree at the [University of Washington School of
Law](https://www.law.uw.edu/academics/mj). We have been covering the
foundational components of the American legal system. One of the things that
came up is the role of the U.S. Constitution in the way modern American society
operates. The Constitution is the foundational document that forms and defines
the American legal system. It’s also one of the few national constitutions that
is composed exclusively of negative law. Negative law expressly limits what the
government is *allowed to do* as opposed to positive law which affirms what the
government *must do*. There is no express responsibility of what the U.S.
federal government *has to do*.

This brings up an issue with national issues that require a larger response like
privacy regulation. The government has to be able to justify that it has the
right to regulate privacy through one of the pre-defined channels mentioned
within the constitution. One of the common ones is the regulation of interstate
commerce. If you read the consent decrees that have been issued to [Facebook](
https://www.ftc.gov/system/files/documents/cases/182_3109_facebook_order_filed_7-24-19.pdf),
[Google](https://www.ftc.gov/sites/default/files/documents/cases/2011/03/110330googlebuzzagreeorder.pdf),
and others, you’ll observe that the angles are often from consumer protection
and misrepresentation to customers and users.

Shifting our perspective, how does this affect privacy engineering and other
forms of risk engineering? Often times it’s tempting to answer these by
restating the negative law-inspired perspective but where does that place our
responsibilities? The goal of privacy engineering is to adversarially look at
data processed within a system and figure out how to protect that data from
misuse and users from harm. If we take the perspective of what we should not do,
it provides a more difficult place for an engineering team to operate from.
Every constraint that’s added increases the complexity of the design and
implementation process.

Building a product or feature works much better when we are able to
affirmatively state what we want to do and what we care about. “What should our
users have?” is an easier question to answer than “What should we not do?”. It
also makes it easier for users to understand what they can expect from us. The
second question is inherently adversarial, it creates combative dynamics when we
engage with teams and puts us in the position where we have to be [The Knights
Who Say Nee](https://www.youtube.com/watch?v=0e2kaQqxmQ0). If we can approach
building products from an affirmative perspective, then it makes it much easier
for users to understand what our values are, it makes risk engineering a lot
more friendly process, and makes it easier to explain to regulators the approach
we’re taking.

So understanding that an affirmative approach to product building makes the most
sense, that leads us to the importance of declaring what our values are and what
we believe users should have. In other words, what ethical guidelines are we
going to follow when building our products. It’s the aggregate of what we choose
to define at the team, org, and company level. Privacy engineering and risk
engineering now shifts to the point of ensuring that we stay consistent with
those values throughout our efforts and initiatives.

Law itself is not a replacement for morality, it’s an expression of a superset
of what we believe are normative behaviors in society. Similarly we have the
opportunity to more proactively state what we believe in and help influence
those societal values. How do those values manifest in our engineering
decisions? Looking within your own projects and teams, how do your group’s
values express hemselves in what you build? That’s what privacy engineering
tries to determine when analyzing a product, what are the values being expressed
in this product and are they compatible with what we believe users should be
entitled to? Because of our unique position as technologists, we have a lot more
power to declare affirmatively what we care about. It’s up to us to determine
how those values are expressed and the way that we affect our world around us.