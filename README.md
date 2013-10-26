# GitMarkdownTools

These are a simple set of tools that I've developed in order to aid myself in writing documents in Markdown while using git as a revision control system.

## Usage

The purpose of these tools are to auto-format markdown code to allow git to show the differences between revisions in a more clear manner.  When git shows differences, it looks at your code line by line.  Since every paragraph in markdown is a single line, this makes differences very difficult to see between revisions, or between uncommitted and committed work.

To solve this, I have created tools that will separate individual sentences into their own lines before a markdown file is committed, and reconstruct paragraphs for work to be done.  The tools will also allow you to perform diffs on uncommitted code using the standard 'git diff' program.

In order for this to work, the tools assume that the author the markdown files is using the common convention of putting two space characters between sentences.  These two spaces are used as delimiters, so if the author is using a different convention, the tools will not function.  The tools also require `perl` to be installed, but if this is a problem, the `perl` components could be easily swapped out for `sed`, `awk`, or some other string manipulation tool.

### Hooks

To accomplish the reformatting when committing and fetching code, I have created two custom git-hooks.  These are the files in the 'hooks' directory.  To use them, place these files into your repository's .git/hooks/ directory (ex: for a repository in `/home/myuser/myrepo`, place them in `/home/myuser/myrepo/.git/hooks/`).  Now whenever you commit your paragraphs will be broken up by sentences, but this will be reversed whenever an author goes to edit the code.  The git-hooks allow for this to be transparent to the author.

### Custom Diff Script

I have also created a custom diff script (git-diff-wrapper.sh) that git must be told to use in lieu of the standard diff utility.  To do this, edit the git configurations of your repository in the .git/config file (ex: for a repository in `/home/myuser/myrepo`, edit `/home/myuser/myrepo/.git/config`).  To call this script instead of the default, add the following configuration:

	[diff]
		external = ./git-diff-wrapper.sh


