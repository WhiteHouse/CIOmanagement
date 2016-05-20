## Management and Oversight of Federal Information Technology

The Federal Information Technology Acquisition Reform Act ([FITARA)](https://www.congress.gov/113/plaws/publ291/PLAW-113publ291.pdf#page=148]), passed by Congress in December 2014, is a historic law that represents the first major overhaul of Federal information Technology (IT) in almost 20 years.  Since FITARA’s passing, OMB published guidance to agencies to ensure that this law is applied consistently governmentwide in a way that is both workable and effective. This guidance is now available as OMB Memorandum M-15-14: Management and Oversight of Federal Information Technology.

OMB used https://management.cio.gov, to collect public feedback on proposed guidance in April 2015. Today this site is still available as a place to continue the discussion of FITARA implementation although the implementation guidance has been finalized. The other pages on [management.cio.gov](https://management.cio.gov) are open for contribution at any time, and are intended to be resources for agencies implementing the FITARA policy.

This repo houses the code for updated guidance and resources. 

### Developing on the site locally

This site uses [Jekyll](http://jekyllrb.com), [Sass](http://sass-lang.com), [Bourbon](http://bourbon.io), [Neat](http://neat.bourbon.io), and requires **Ruby 2.x**.

Install dependencies with Bundler:

```
bundle install
```

Start up a Sass watcher to keep assets auto-compiled:

```
make watch
```

And run the site with Jekyll:

```
bundle exec jekyll serve --watch
```

If all goes well, visit the site at `http://localhost:4000`.

### Public domain

This project is in the worldwide [public domain](LICENSE.md). As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
