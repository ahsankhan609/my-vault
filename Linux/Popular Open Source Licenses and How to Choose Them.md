---
title: Which License to Use for Open Source Projects?
source: https://itsfoss.com/open-source-licenses-explained/
author:
  - "[[Sylvain Leroux]]"
published: 2017-02-26
created: 2026-05-29
description: This detailed guide gives an effective Open Source license comparison. It should help you choose the right Open Source license for your project.
tags:
  - license
  - open-source
  - github
---
So, you’re working on that cool new project for a while — and you’re ready now to make the critical move from *closed source* to *open source*.

It doesn’t seem much more work than cleaning the sources and the commit history before pushing your repository onto [GitHub](https://github.com/?ref=itsfoss.com) or [Bitbucket](https://bitbucket.org/?ref=itsfoss.com) … … until the question of the License pops out. There are so many choices available. Which one to choose? And do you *really* need a License after all?

The short answer to that latter question is easy: Yes, you *really* need a License. As about what License you need, I can even make a shorter answer: *it depends*.

But if you’re serious about your project, you probably want a little bit more details. So read ahead — and remember: you’re entering holy war territory now!

## Do I need a License? And what is a License after all?

A License is an *official* permission granted by the owner of some Work (the “Licensor”) to other people (the “Licensee”) and governing how the Licensee is allowed to use the Licensor’s Work.

This takes the form of a contract, both parties has to agree with. Nowadays, the acceptation is rather implicit: just by *using* some Work, you are reputed to agree with its usage License.

Just to make thinks clear, when releasing your *own* work, the Licensor is *you*. And the Licensee, *anyone* using your code. Broadly speaking, this includes two main categories: *developers* and *end users*.

And to fix few more vocabulary terms, by *modifying* your Work, a Licensee is creating what is called a Derivative Work. Not all licenses agree though if the *use* of your Work in a larger work will qualify that latter as a Derivative Work or not. As you will see below, some licenses specifically address those issues.

## What is the purpose of the License?

Basically, the License is a way for the Licensor and the Licensee to agree on the *rights and obligations* of *both* of them. Those rights and obligations associated with a License can be anything — *up to the extent of what’s allowed by the Law*. For example, a Licensor might require the Licensee to quote her name when using her work. Or can authorize to copy her work, but not to modify it in any way. Or even require Derivative Work to be released under the same terms as the original Work.

On the other hand, the License is a way to protect the Licensee too. By clearly stating how he can use your Work, he is not at risk of seeing you unexpectedly asking for royalties or another form of compensation for having used your work. Something that is critical for your Work adoption.

So, the License will protect your work. Will protect the Licensor. But will protect you too. I mean you, *personally*. For example by limiting the Licensor’s responsibility for potential damages caused by her work.

## And what if I don’t use any License at all?

In absence of a License explicitly associated with a Work, the “default” copyright for the author’s jurisdiction applies. In other words, *never* consider the “absence of license” as an implicit grant for us to do whatever we want with your work. This is the exact opposite: without any specific license, you, the author, didn’t waive ANY of your rights as granted by the law.

But always remember a License governs rights *and* obligations. Did you ever wonder why so many License text contains a disclaimer written in ALL UPPERCASE LETTERS about the guarantees provided with a product — or more often the absence of guaranty? This is to *protect* the owner of the work against implicit guarantees or user assumptions. The last thing you want is to be sued as a consequence of releasing your work open-source!

## Can I use a custom License?

Yes, you can. But you probably shouldn’t.

Being a contract, a License cannot (in most jurisdictions? all of them?) take precedence over the territorial laws. Hence the difficulty enforcing the licensing rights in a globalized world. It would be probably easier (I mean, less difficult) to defend a “standard” License before a judge. In fact, such cases have already been defended in several jurisdictions and may be cited as precedent. Obviously, something that can’t be done with a Custom License.

In additions, Custom Licenses (sometimes nicknamed [Vanity Licenses](https://en.wikipedia.org/wiki/License_proliferation?ref=itsfoss.com#Vanity_licenses)) may create incompatibilities with other licenses, resulting in a poor compatibility of your Work legally speaking.

## May I use several Licenses?

Yes. Multi-licensing — notably Dual-licensing — is not that uncommon. This is especially true when you want to build a business around your free Work. In that case, your project will probably be released both under some FOSS license and a commercial license.

Another use of multi-licensing is to increase compatibility, by allowing your Work to be combined with works published under different terms or to satisfy different user needs or requirements. This is a reason why some project are released under several FOSS licenses.

But be warned: not all licenses are compatible together! Once again, I would discourage you from reinventing the wheel by staying with well-known compatible licenses if you want to go that way.

## Can I change the License “later”?

Yes. The copyright holder is responsible for the licensing terms. It is rather easy to change the License as long as you are the only contributor. But to take an extreme example, if Linus Torvald would want to release the Linux Kernel under a different license, he would probably need first the agreement of the thousands of contributors to that project. Something impossible in practice.

For a more reasonably sized project, it can be done. And in fact, it was as you will see in some examples below.

## Which Open Source License should I use?

Ok, now, you’re convinced you should use a Standard License. But Which one to choose? The final choice is up to you. And there are very well made comparators available on the web to help you in your choice. Just to quote my favorites:

- [http://oss.ly/licdif](http://oss.ly/licdif?ref=itsfoss.com)
- [https://choosealicense.com/](https://choosealicense.com/?ref=itsfoss.com) / [https://choosealicense.com/appendix/](https://choosealicense.com/appendix/?ref=itsfoss.com)
- [https://opensource.org/licenses](https://opensource.org/licenses?ref=itsfoss.com)
- [https://tldrlegal.com/](https://tldrlegal.com/?ref=itsfoss.com)

But as always with legal affairs, the definitive answer will be to read — and understand — the authoritative text of the License. That may require the help of a professional lawyer. Something I am not.

But what I can do is providing you some introduction to the most common Licenses in order to guide your first steps.

### GNU General Public License (GPL)

The GPL is one of the most popular Open Source License. It comes in several versions — but for a new project, you should consider the most recent, which is the [GPL 3](https://www.gnu.org/licenses/gpl-3.0.en.html?ref=itsfoss.com) at the time of this writing.

Supporting a strong [copyleft](https://en.wikipedia.org/wiki/Copyleft?ref=itsfoss.com), the GPL is probably the most protective free software license. Something it can be praised or criticized for depending your point of view. The core concept behind the GPL being *any* Derivative Work must be released under the GPL too.

- **Strong copyleft**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must release the source alongside with Derivative Work.
- Derivative Work must be released under the same terms.

**Popular projects**

The GPL is the natural license for the projects of the Free Software Foundation. Including the [GNU tools](https://www.gnu.org/?ref=itsfoss.com) at the heart of any Linux system. Large projects — *a fortiori* commercial ones — tend to use the GPL in conjunction with one or several other Licenses.

- [Inkscape](http://wiki.inkscape.org/wiki/index.php/Frequently_asked_questions?ref=itsfoss.com#Under_what_license_is_Inkscape_released.3F) (Vector drawing): GPLv2
- [Drupal](https://www.drupal.org/about/licensing?ref=itsfoss.com#q1) (Web Content Management System): GPLv2
- [MariaDB](https://mariadb.com/kb/en/mariadb/licensing-faq/?ref=itsfoss.com) (Databases): GPL v2
- [MySQL](https://mariadb.com/kb/en/mariadb/licensing-faq/?ref=itsfoss.com) (Databases): GPL and Commercial License
- [Qt](https://www.qt.io/licensing/?ref=itsfoss.com) (cross-platform application framework): LGPL, GPL, and Commercial — depending the modules and service-agreement level

### GNU Lesser General Public License (LGPL)

The GPL is very restrictive in the sense it forces any Derivative Work to be released open-source under the same terms. This is especially a concern for libraries — which are building blocks for larger software: by releasing a library under the GPL, you will force any application *using* that library to be released as GPL too. Something the LGPL addresses.

For libraries, the FSF [distinguishes three cases](https://www.gnu.org/licenses/license-recommendations.en.html?ref=itsfoss.com):

- Your library implements a standard that competes with a non-free standard. In that case, wide adoption of your library will help the Free Software cause. The FSF suggests the quite permissive Apache License for that case (described later in that article).
- Your library implements a standard already implemented by other libraries. In that case, there is no benefit for the Free Software cause to abandon copyleft entirely. So the FSF recommends the LGPL.
- Finally, if your library does *not* compete with other libraries nor other standards, [the FSF recommends the GPL](https://www.gnu.org/licenses/why-not-lgpl.en.html?ref=itsfoss.com).

The FSF arguments are mostly ethical and philosophical. In practice, developers may have other concerns. Especially if they plan to develop a business based on the licensed work. Once again, dual-licensing may be an option to consider.

- **Weak copyleft (bound to dynamically linked library)**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must release the source alongside with Derivative Work.
- if you *modify* the Work, you *must* release the Modified Work under the same terms.
- if you *use* the Work, you \_don’t need\_to release the Derivative Work under the same terms.

**Popular projects**

- [OpenOffice.org 3](https://www.openoffice.org/license.html?ref=itsfoss.com) (office suite): LGPLv3 — but Apache OpenOffice 4 switched to Apache License 2.0.
- [GTK+, the GIMP Toolkit](https://www.gtk.org/?ref=itsfoss.com) (GUI toolkit): LGPLv2.1
- [CUPS](https://www.cups.org/doc/license.html?ref=itsfoss.com) (cross-platform printing system): GPL or LGPLv2 with an exception for Apple operating systems — depending the components.
- [WineHQ](https://www.winehq.org/license?ref=itsfoss.com) (Windows compatibility layer): LGPLv2.1
- [GNU Aspell](https://directory.fsf.org/wiki/Aspell?ref=itsfoss.com#tab=Details) (Spell checker): LGPLv2.1

### Eclipse Public License (EPL 1.0)

![Eclipse Open Source License](https://itsfoss.com/content/images/wordpress/2017/02/eclipse-license-800x188.png)

Eclipse Open Source License

With a weaker copyleft than the LGPL, the Eclipse License is more Business-Friendly as it allows sub-licensing and building of software made of EPL and non-EPL (even proprietary) licensed code, provided the non-EPL code is a *“separate module\[s\] of software”*.

In addition, the EPL adds extra protection for the EPL code contributors in the case of lawsuits/damages caused by a commercial offering including that Work.

- **Weak copyleft (bound to software “module”)**
- The Work is suitable for commercial use.
- The Licensees can modify the work.
- If you *modify* the Work, you *must* release the Modified Work under the same terms.
- If you *use* the Work, you \_don’t need\_to release the Derivative Work under the same terms.
- Commercial distributors of the software must defend or compensate original EPL contributors from lawsuits/damages caused by the commercial offering.

**Popular projects**

Obviously, the EPL is the natural license for the projects of the Eclipse Foundation. Including the popular Eclipse IDE. But it gained some popularity beyond that — especially in the Java world:

- [Clojure](https://clojure.org/community/license?ref=itsfoss.com) (Programming language)
- [Graphviz](http://www.graphviz.org/License.php?ref=itsfoss.com) (Graph visualization package)
- [Jetty](http://www.eclipse.org/jetty/licenses.html?ref=itsfoss.com) (Application server): dual license EPL1.0/Apache License 2.0 since Jetty 7
- [JUnit](http://junit.org/junit4/license.html?ref=itsfoss.com) (Java unit testing framework)

### Mozilla Public License (MPL)

![Mozilla License](https://itsfoss.com/content/images/wordpress/2017/02/jb_Mozilla_D_protocol_1-800x264.jpg)

Mozilla License

The Mozilla Public License is license used for software developed by the Mozilla foundation. But it’s certainly not limited to that area. The MPL aims at being a compromise step between strict licenses (like the GPL) and permissive licenses (like the MIT License).

In the MPL the “licensing unit” is the source file. Licensors are not allowed to restrict the user rights and access on any file covered by the MPL. But the same project can also contain proprietary non-MPL licensed files. The resulting project can be released under any license, provided that access to the MPL licensed files is granted.

- **Weak copyleft (bound to individual files)**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must provide proper attribution for the Work.
- Licensees may redistribute Derivative Work under different terms
- Licensees cannot relicense MPL-licensed source
- Licensees must distribute MPL-licensed source code alongside with their Derivative Work.

**Popular projects**

- Mozilla Firefox(web browser), Mozilla Thunderbird(email client): MPL
- [LibreOffice](https://www.libreoffice.org/about-us/licenses/?ref=itsfoss.com) (office suite): MPL2.0
- [H2 Database Engine](http://www.h2database.com/html/license.html?ref=itsfoss.com) (database): MPL2.0 and Eclipse License 1.0
- [Cairo](https://cairographics.org/?ref=itsfoss.com) (2D graphic engine): MPL 1.1 or LGPLv2.1

### Apache License 2.0 (ASL 2.0)

![Apache license](https://itsfoss.com/content/images/wordpress/2017/02/apache-license-800x210.png)

Apache license

With the ASL, we are entering the realm of *permissive* free licenses. But even the FSF suggest Apache License in some cases. The Apache License is permissive as it does not require *any* Derivative Work to be distributed under the same terms. In other words, this is a non-copyleft license.

The ASL is the only license used for projects of the Apache Software Foundation. Being considered as business-friendly, it has gained widespread adoption outside of that organization. It is not uncommon to see enterprise-grade projects to be released under the ASL.

- **Non-copyleft**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must provide proper attribution for the Work.
- Licensees may redistribute Derivative Work under different terms.
- Licensees do not have to distribute the source code alongside with their Derivative Work.

**Popular projects**

- [Android](https://source.android.com/source/licenses.html?ref=itsfoss.com) (operating system): ASL 2.0 with some exceptions (notably regarding the Linux kernel)
- [Apache httpd](https://httpd.apache.org/?ref=itsfoss.com) (Web server): ASL 2.0
- [Apache Spark](http://spark.apache.org/faq.html?ref=itsfoss.com) (Cluster computing framework): ASL 2.0
- [Spring Framework](https://projects.spring.io/spring-framework/?ref=itsfoss.com) (Framework for Java-based enterprise applications): ASL 2.0

### MIT License

This one is a very popular license. Even probably the most popular one. By putting very few limitations on reuse, the MIT License can easily be associated with other licenses, from the GPL to proprietary licenses.

- **Non-copyleft**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must provide proper attribution for the Work.
- Licensees may redistribute Derivative Work under different terms
- Licensees do not have to distribute the source code alongside with their Derivative Work.

**Popular projects**

- [node.js](https://nodejs.org/en/?ref=itsfoss.com) (JavaScript runtime environment): MIT License
- [jQuery](https://jquery.com/?ref=itsfoss.com) (client-side JavaScript library): MIT License (until 2012, dual-license MIT/GPL)
- [Atom](https://atom.io/faq?ref=itsfoss.com) (text editor): MIT License
- [AngularJS](https://docs.angularjs.org/misc/faq?ref=itsfoss.com) (JavaScript application framework): MIT License
- [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/copyright.html?ref=itsfoss.com) (SQL toolkit and Object Relational Mapper for Python): MIT License

### BSD Licenses

BSD License comes in three flavors. The original 4-clause License, the “revised” 3-clause License and the “simplified” 2-clause License. All in spirit are very close to the MIT License. And indeed, there is very little practical differences between the 2-clause BSD License & the MIT License.

3- and 4-clause BSD Licenses add more requirements concerning name reuse and advertising. This is something to consider if you want to protect your product or brand name.

- **Non-copyleft**
- The Work is suitable for commercial use.
- Licensees can modify the work.
- Licensees must provide proper attribution for the Work.
- Licensees may redistribute Derivative Work under different terms.
- Licensees do not have to distribute the source code alongside with their Derivative Work.
- Licensees cannot use the original Author name or trademark to endorse Derivative Work (3- and 4- clause BSD)
- Licensees must acknowledge the original Author in all advertising materials mentioning features or use of the Work (4-clause BSD)

**Popular projects**

- [Django](https://www.djangoproject.com/foundation/faq/?ref=itsfoss.com) (web ramework): 3-clause BSD
- [Redis](https://redis.io/topics/license?ref=itsfoss.com) (data store): 3-clause BSD
- [Ruby](https://www.ruby-lang.org/en/about/license.txt?ref=itsfoss.com) (programming language): 2-clause BSD and custom license
- [Nginx](http://nginx.org/LICENSE?ref=itsfoss.com) (Web server): 2-clause BSD
- [NetBSD](http://www.netbsd.org/about/redistribution.html?ref=itsfoss.com) (Operating system): 2-clause BSD — 4-clause BSD until 2008

## The last word on Open Source licenses

If you come that far, congratulations! You understand it now, *licensing* is really a huge *and* complex topic. But it worth taking the time to choose the right license for your project — and to make that choice early. It could save you lots of problems later, so you can use your time and energy working on your project rather than dealing with copyright or legal compatibility issues.

Even if I’ve done my best to make that topic accessible, it is not always easy to summarize the subtleties of the various licenses. And beyond the few major licenses presented here, there are [dozens of others more or less commonly used](https://www.blackducksoftware.com/top-open-source-licenses?ref=itsfoss.com).

So, don’t hesitate to use the comment section below to tell us what’s *YOUR* preferred license and why. Or to mention some important characteristics I might have forgotten!