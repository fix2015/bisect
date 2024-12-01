# Quick Git Bisect Example

## Scenario:
You know a bug was introduced somewhere between two commits. One commit is working fine (good), and the other is failing (bad). You need to find the exact commit that introduced the bug.

## Steps:

1. **Start the bisect process**:  
   First, tell Git which commit is good and which one is bad.
   ```bash
   git bisect start
   git bisect bad HEAD         # Mark the current commit (HEAD) as bad
   git bisect good <good_commit_hash>  # Mark a known good commit
   ```

   For example:
   ```bash
   git bisect bad HEAD
   git bisect good 7907b1b    # The first commit is known to be good
   ```

2. **Git will check out a commit halfway between the good and bad commits**.  
   Test the code to see if the bug still exists.

3. **Mark the result**:
   - If the bug exists, mark the commit as **bad**:
     ```bash
     git bisect bad
     ```
   - If the bug does **not exist**, mark the commit as **good**:
     ```bash
     git bisect good
     ```

4. **Repeat the process**:  
   Git will continue narrowing down the range, checking out commits in the middle, until it finds the first bad commit.

5. **Once found**, Git will tell you the exact commit that introduced the bug:
   ```bash
   <commit_hash> is the first bad commit
   ```

6. **Finish the bisect process**:  
   After finding the bad commit, run:
   ```bash
   git bisect reset
   ```
   This returns you to the branch you were on.

---

## Example in Action:
```bash
$ git bisect start
$ git bisect bad HEAD
$ git bisect good 7907b1b
# Git checks out a commit halfway between 7907b1b and HEAD
# Test the code, then mark the commit:
$ git bisect bad
# Repeat until Git identifies the bad commit
$ git bisect reset
```

## Automated Testing (optional):
If you have an automated test to detect the bug, you can run `git bisect` with a test script:
```bash
git bisect run ./test-script.sh
```

This will automatically run your script and mark commits as good or bad based on the test result.

---

For a more in-depth explanation and smarter approaches to bug localization with Git Bisect, check out my full article:  
[**Debugging with Git Bisect: A Smarter Approach to Bug Localization**](https://medium.com/@vitaliisemianchuk/debugging-with-git-bisect-a-smarter-approach-to-bug-localization-e550da92e19a)

## Connect with Me:
- [LinkedIn - Vitalii Semianchuk](https://www.linkedin.com/in/vitalii-semianchuk-9812a786/)
- [Telegram - @jsmentorfree](https://t.me/jsmentorfree) - We do a lot of free teaching on this channel! Join us to learn and grow in web development.

## License

MIT License  
Copyright (c) 2024 Vitalii Semianchuk  

[LinkedIn Profile](https://www.linkedin.com/in/vitalii-semianchuk-9812a786/)