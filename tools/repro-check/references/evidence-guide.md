# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:**  
In an eval package, look at the repro report's environment record, the issue context, and the repo-facts block. In live mode, look at the student's draft reproduction comment together with the issue and the repository's setup documentation.

**What good looks like:**  
The report identifies the environment needed to understand the reproduction, such as relevant software or dependency versions, operating system, runtime, or configuration. The environment should match the issue's stated target, or any difference should be clearly identified.

## Steps

**Where it lives:**  
In an eval package, look at the reproduction steps in the repro report and compare them with the issue context. In live mode, look at the steps in the student's draft comment and the repository's setup or usage documentation.

**What good looks like:**  
The steps give enough information for another person to start from a known state and reach the behavior being tested. Important commands, inputs, configuration, or actions needed to trigger the behavior are included.

## Behavior shown

**Where it lives:**  
Look at the artifacts in the repro report, including output excerpts, logs, error messages, screenshots, test results, or other observable results, and compare them with the behavior described by the issue.

**What good looks like:**  
The artifact shows the same behavior described by the issue rather than a different or related problem. The evidence should make it possible to connect the observed result to the reported bug.

## Honesty

**Where it lives:**  
Compare the reproduction report's conclusion and claims with its steps, environment information, and artifacts.

**What good looks like:**  
The report states only what the evidence supports. A successful reproduction should have evidence showing the reported behavior. A cannot-reproduce result is acceptable when the attempts and observed results are clearly documented without claiming the bug does not exist.

## Comms

**Where it lives:**  
In an eval package, look at the claim comment and reproduction report together with the repo-facts block and any stated contribution or communication policies. In live mode, compare the student's draft comments with the issue thread, repository templates, contribution guide, and any AI-use disclosure requirements.

**What good looks like:**  
The claim identifies the specific issue and clearly states what the contributor plans to investigate without promising a fix or deadline. The reproduction comment is specific to the issue, accurately describes what was tested, follows the repository's stated conventions, and includes any required disclosures.
