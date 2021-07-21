[![Build Status](https://msmobilecenter.visualstudio.com/Mobile-Center/_apis/build/status/office-contact-card?branchName=master)](https://msmobilecenter.visualstudio.com/Mobile-Center/_build/latest?definitionId=3232?branchName=master)

# Office Contact Card

Contact card in Office style is a React component, which provides contact card UX with information from your Azure Active Directory.

![Preview](https://github.com/Microsoft/contact-card/blob/master/sample/i/preview.png)

Main functionality:
* Avatar preview
* Name and title resolution
* Hover card with:
  * Contact info summary
  * Manager summary
  * Contact info details
  * Full organization hierarchy
  * People navigation history


# How to Use it

## Installation

```shell
npm i office-contact-card
```

## Authentication

The component requires access to [MS Graph](https://developer.microsoft.com/en-us/graph).

## Example

```typescript
import { GraphServiceAuthenticator, PersonaWithCard, PersonaShowMode } from "office-contact-card";

GraphServiceAuthenticator.setAuthCallback(() => Promise.resolve("-token-") );

function renderCard() {
  return <PersonaWithCard email={"test@fabricam.com"} showMode={PersonaShowMode.NameTitle} />;
}
```

# Development within a dependent project

It may be handy to develop office-contact-card within the context of a dependent project or library. 

## Prerequisites 

- [Python 2.7](https://www.python.org/download/releases/2.7/)
- msbuild.exe, specifically the 2017 version. Either obtainable through downloading and installing [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/) with the "Desktop development with C++" workload or running `npm i -g windows-build-tools`

## How-to

First clone or download office-contact-card to a folder

`git clone https://github.com/microsoft/contact-card.git`

Install and build this component

`cd contact-card && npm install && npm run build`

Next create a symlink into the global node_modules folder using [npm link](https://docs.npmjs.com/cli/v6/commands/npm-link). To ensure the app [has no duplicate React](https://reactjs.org/warnings/invalid-hook-call-warning.html#duplicate-react) perform the link against your projects specific version of React. This command may require a force, which can be accomplished by appending a `-f`

`npm link ..\..\my-project-using-contact-card\src\node_modules\react\` 

Navigate back to the dependent project

`cd C:\workspace\my-project-using-contact-card`

And use the linked office-contact-card

`npm link office-contact-card`

Restart your application and your project will now be using your locally installed office-contact-card repository. 

You can run `npm list -g --depth=0 --link=true` to verify the symlink is working properly. That command should output something like the following: 

```
C:\Program Files\nodejs -> .\
+-- office-contact-card@2.1.0 -> .\..\..\path\to\your\local\contact-card
```

## Reloading changes to contact-card

After every change done to the local office-contact-card a subsequent `npm run build` needs to be done within the contact-card folder.

## Clean-up

Once you've completed changing office-contact-card and want to revert the symlink run the following from your dependent project directory

`npm unlink --no-save dependency`

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
