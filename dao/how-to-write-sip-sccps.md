# How to write SIP/SCCPs

SIPs are the official documentation used to present potential changes to the core protocol. Anyone can propose a SIP, but the Spartan Council ultimately decides on approval or rejection. There are also SCCPs, or Synthetix Configuration Change Proposals. SCCPs follow the same process as a SIP, but they are proposals to update the parameters of the protocol, such as adjusting the C-Ratio required for stakers or the amount of fees collected from trading.

## **How to use GitHub to submit a Synthetix Improvement Proposal (SIP or SCCP)** <a href="#bda6" id="bda6"></a>

<figure><img src="https://miro.medium.com/max/875/0*xoOJQWVPJXEl4-j6" alt=""><figcaption></figcaption></figure>

The Synthetix community allows anyone to submit a proposed change to the platform in the form of a SIP (Synthetix Improvement Proposal), even if they are not staking and don’t have the ability to vote. Synthetix is a complicated protocol with a sophisticated governance structure that’s as decentralized as possible while remaining efficient and effective, so the process for managing proposals must be robust enough to filter out unnecessary or underdeveloped ideas. Synthetix uses GitHub, a popular platform chosen by software development teams to submit and develop projects and collaborate, to manage SIPs submitted by the community.

## Github SIP/SCCP Creation Tool - Made by SNX Grants Council

Instead of using GitHub directly, the grants council has funded an easy to use tool to submit a SIP/SCCP through a web interface, which will then post it for you on the SIP repository.

{% embed url="https://pr.synthetix.io/" %}

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## Github SIP/SCCP Guide

While GitHub can be intimidating to unfamiliar users, hopefully this document can serve as a guide and encourage participation in the governance process. The transparency and ability to audit changes make GitHub a natural choice to manage SIPs. By creating and managing repositories, branches, commits and pull requests, users can collaborate on projects and track changes as they go. Here’s the basic flow:

* **Repositories**- A repository is used to organize a single project. They contain folders, files, data sets, images, etc. To submit a SIP, you must fork Synthetix’s repository. This makes a distinct copy of the entire project at the moment you fork.
* **Branches**- Branches are different versions within a repository. While a fork is a completely separate copy, a branch remains part of the original repository. Teams use branches to work on bugs/enhancements while keeping any potentially harmful changes separate from the main project.
* **Commits**- Once a branch is complete, you must commit those changes back to the main branch for review.
* **Pull requests**- A Pull Request is the submission of proposed changes that will be reviewed before being merged into the main branch. A pull request will display any changes from the main branch by highlighting those lines in green, while any differences from the main branch are highlighted red.

<figure><img src="https://miro.medium.com/max/875/0*OFGjACEsc2Bl1rmB" alt=""><figcaption></figcaption></figure>



## **Submission** <a href="#562f" id="562f"></a>

Once you’ve groomed your proposal with the help of the community and you’ve built up excitement and momentum, you’re ready to create your proposal. Here are the stages a proposal will go through once submitted:

<figure><img src="https://miro.medium.com/max/751/0*lDZh6f71DIb0GSrl" alt=""><figcaption></figcaption></figure>

1. **Draft**- SIP is a work-in-progress or under review
2. **Feasibility**- SIP has been assigned to a Core Contributor who is working to determine how likely it is to succeed
3. **SC Review Pending**- SIP is under formal review by the Spartan Council. Once complete the SIP is ready for voting or sent back to feasibility
4. **Vote Pending-** SIP is featured on the [staking site](https://staking.synthetix.io/gov) for community members to vote on
5. **Approved**- SIP has passed community governance and is in development, or **Rejected**- The SIP has failed to reach community consensus
6. **Implemented**- the SIP has been deployed to mainnet

## **Formatting** <a href="#1020" id="1020"></a>

This is when you will create the actual proposal in the correct format so you can submit it to the Synthetix GitHub repository. The structure of a SIP is based on the EIP Ethereum Improvement Proposal, which is based on Bitcoin’s BIP Bitcoin Improvement Proposal, which is based on Python’s PEP Python Enhancement Proposal

<figure><img src="https://miro.medium.com/max/506/1*VPW2kDnalUO-DY8eIqNxcQ.gif" alt=""><figcaption></figcaption></figure>

The first step is to review the formatting requirements listed in [SIP-1](https://sips.synthetix.io/sips/sip-1). You can also view [all SIPs here](https://sips.synthetix.io/all-sip/) and reference format and content. If you click on the title of a SIP you’ll be directed to a document in the Synthetix GitHub Repository. Submitter’s are encouraged to reach out to experienced community members for assistance with writing a SIP. Ask around in the [Synthetix Discord](https://discord.gg/Hf9A3tq) and someone is sure to jump in and help out.

When writing a SIP, you can start with this [SIP template](https://github.com/Synthetixio/SIPs/blob/master/sip-x.md). You’ll notice the format is very specific:

<figure><img src="https://miro.medium.com/max/875/0*qPB1iwQDrSBfyEQZ" alt=""><figcaption></figcaption></figure>

SIPs must be written in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format. Review the link for in-depth explanation of markdown, but here are the basics:

**Headers** must be denoted with #’s

* \# H1
* \## H2
* \### H3

**Emphasis** is applied using \*, \_, and \~

* _Emphasis/italics_, with \*asterisks\* or \_underscores\_.
* **Strong emphasis/bold**, with \*\*asterisks\*\* or \_\_underscores\_\_.
* _**Combined emphasis**_ with \*\*asterisks and \_underscores\_\*\*.
* Strikethrough uses two tildes. \~\~Scratch this.\~\~

**Lists** must be ordered as follows:

* 1\. First ordered list item
* 2\. Another item
* ⋅⋅\* Unordered sub-list.
* 1\. Actual numbers don’t matter, just that it’s a number
* ⋅⋅1. Ordered sub-list
* 4\. And another item.
* You must separate elements with commas

**Dates** must follow the ISO 8601 format (yyyy-mm-dd)

**Links** must be embedded using \[ ] and ():

* For a link to the \[synthetix staking site]\(https://staking.synthetix.io), use this format
* Which ends up looking like this:
* For a link to the [synthetix staking site](https://staking.synthetix.io/), use this format

**Tables** should be formatted using | as follows:

* Markdown | Less | Pretty
* — — | — — | — -
* \*Still\* |\`renders\`| \*\*nicely\*\*
* 1 | 2 | 3

<figure><img src="https://miro.medium.com/max/429/0*CVBcVBm6G-pLGdpX" alt=""><figcaption></figcaption></figure>

**Images**

* Include image files in a subdirectory of the Pull Requests “Asset” folder: assets/sip-X
* Use relative links when linking to an image: ../assets/sip-X/image.png

## What to include in a SIP <a href="#2a55" id="2a55"></a>

A successful SIP will include the following sections

1. A **Preamble**, done in RFC 822 style This is an internet standard syntax for text based email messages.

<figure><img src="https://miro.medium.com/max/621/0*tBstMmEGbcclpMSq" alt=""><figcaption></figcaption></figure>

Include headers in the preamble with metadata for the SIP in the following order:

* SIP Number: This will be determined by the SIP editor on submitted
* Title: A short concise title (maximum of 44 characters)
* Author: The Author’s name, Username, email address, etc, formatted as follows: “Submitters Name/moniker” \<emailaddress@dom.ain> to include email. “Submitter’s Name/moniker” (@username)
* Discussions-to: \<URL to a discussion forum, open github issue, or discord conversation with the greater community> \*Optional, but very important
* Status: Start in \<Draft> status
* Created Date: In “yyyy-mm-dd” format, e.g. 2001–08–14
* Updated Date: When substantial changes have been made to the SIP during the Draft phase. \*Optional.
* Requires: \<SIP number(s)> SIPs that this SIP is dependent on. \*Optional

2\. A **Simple Summary** of the proposal that a layman could understand. Save technical details for specification

3\. An **Abstract**, which is a short \~ 200 word description of the SIP that lays out the technical solution being proposed. This describes what will be done if implemented, not why or how it will be done.

4\. The **Motivation** for the SIP. This is the problem statement or the Why. For SIPs that aim to change the protocol, the motivation should explain the issue/inadequacy, how it is not being addressed properly, and why this change is necessary. While optional, some SIPs could be rejected simply because a proper motivation was not included

5\. The **Specification** is where you can get technical. Include the syntax, semantics, and any technical definitions or concepts necessary to understanding the scope and desired impact to the system. Included in the specification is:

* An **Overview**, which is a high level summary of how this solution will improve the protocol, and how these features will be implemented.
* The **Rationale** for the change, which builds on the specification and design of the solution and justifies specific decisions. Alternate designs/approaches should be included with explanations why they are not sufficient as well as any modifications needed for practical application (such as language requirements). Rationale can also act as a record of community consensus, including a summary of discussion with both support and opposition.
* A **Technical Specification** that includes an outline of the public API of the proposal. You should also describe any changes to UI that is currently user facing.
* **Test Cases** to be applied during the Implementation phase.

6\. A Copyright Waiver as all SIPs must be public domain.

Any files, such as diagrams, tables, etc. that accompany a SIP should be named as follows:

SIP-XXX-Y.ext

* XXX= SIP number
* Y= serial number starting at 1
* ext= file extension, such as “.png”

## Adding a SIP to the Repository <a href="#c826" id="c826"></a>

Once you’ve written your SIP and included all the components above, you are ready to begin the process of adding your SIP to the [Synthetix repository](https://github.com/Synthetixio/SIPs/tree/master/content/sips). First, you must fork the repository by clicking on the “Fork” button in the top right:

<figure><img src="https://miro.medium.com/max/875/0*43c0wV4G-kENmdNl" alt=""><figcaption></figcaption></figure>

Now you’ll see your copy of the repository:

<figure><img src="https://miro.medium.com/max/729/0*Xh8dPyAUpV585E7V" alt=""><figcaption></figcaption></figure>

Next, add your SIP to your fork. Create a new branch by clicking on the “master” dropdown. Type in the name of your SIP (The title formatted as described above) and then click on “create \[SIP name] from ‘master’”:

<figure><img src="https://miro.medium.com/max/690/0*eFlBTs1FNkV71A-R" alt=""><figcaption></figcaption></figure>

From the new branch. Click "Content" then "SIP"

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Now click on the “Add file” dropdown and select “Create new file” or “Upload files”:

<figure><img src="https://miro.medium.com/max/875/0*Fgz458_wyL__uwYt" alt=""><figcaption></figcaption></figure>

Enter the Name/Title of the SIP. Use an abbreviated filename such as “sip-draft\_title\_abbrev.md, with a maximum of 44 characters. Next, add the content of your SIP under the “<> Edit new file” tab:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Once complete, select the “Create a new branch for this commit and start a pull request.” radio button and click the green “Propose new file” button:

<figure><img src="https://miro.medium.com/max/875/0*omlYgK9hNVGlR-9k" alt=""><figcaption></figcaption></figure>

Your First pull request should be the first draft of your final SIP, so make sure it’s complete.

## Editor Review of your Draft SIP

Congratulations, you submitted a SIP! From here your SIP will go to a SIP Editor who manually reviews it, assigns a SIP number and then accepts the merge. Editors analyze the SIP to ensure that its sound and complete. It must be able to hold up to basic technical scrutiny, it must have an appropriate title and it must include the correct format for grammar, markdown and code style. SIP editors will correct errors in structure, grammar, spelling or markup where they can. They don’t look at SIPs with a critical eye at this stage, only as an administrator and editor.

If your SIP is not ready in the eyes of the editor, they will send it back to the author with instructions for how to revise it. If your SIP is deemed ready, it is now assigned a number (generally the pull request number or issue number) and merges the pull request into the main repository. Once ready for the next steps, the Editor will message the author and provide further instructions.

And that’s it. The fate of your precious SIP is now in the gentle hands of experienced editors. They will work to complete a feasibility study and if successful, move the SIP to the voting stages.
