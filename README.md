# Deta Deploy

Deploy code to a [Deta](https://deta.sh) Micro.

NOTE: This Action resolves [issues](https://github.com/BogDAAAMN/deta-deploy-action/issues/5) faced by [the Action it was based off of](https://github.com/BogDAAAMN/deta-deploy-action).

<p align="center">
 <i>Lots of thanks to the <a href="https://github.com/Maxsior/BotCom">BotCom</a> folks for clarification and to the <b><a href="https://deta.sh">Deta</a> folks</b> and for all the walkthroughs and hard work! 💕</i>
</p>

## Usage

This is a simple GitHub Action to deploy current repo to a Deta Micro. Uses `deta deploy` command to deploy the latest changes as per [documentation](https://docs.deta.sh/docs/cli/commands/#deta-deploy).

## Inputs

### `deta-access-token`

**Required**. The access token generated by Deta. Used for `deta clone` and `deta deploy` commands.

You can generate your own access token from your [Deta account](https://web.deta.sh/home/) in order to avoid web login. Follow the Authetication documentation [here](https://docs.deta.sh/docs/cli/auth).

⚠️ Be **very** sure you don't share the token or paste it in plain text! You can add it to the GitHub project's secrets as it follows:

- On your project's page click on the **Settings** button;
- Navigate to **Secrets** panel;
- Click on **New secret**;
- Name it `DETA_TOKEN` and paste the key there.

Now you can use the key in your project's actions as `${{ secrets.DETA_TOKEN }}`. Read more about [GitHub Secrets](https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets).

![GitHub Visual Instructions](https://github.com/BogDAAAMN/copy-sentiment-analysis/blob/v0.6.1/_static/gif/github.gif)

### `deta-name`

**Required**. The name of the existing Deta Micro you are deploying to. Used for `deta clone` command in order to retrieve the latest information about the targeted Micro.

### `deta-project`

The name of the Deta project your Micro is part of. Used for `deta clone` command in order to retrieve the latest information about the targeted Micro. Default `"default"`.

### `deta-project-dir`

The name of the directory where the Deta code is located, in cases where the project is not located in the root directory. Default `.` (the root)

## Example action workflow

```yaml
name: Deploy to Deta
on: push

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2 #Be sure you check-out the repo first. Deta CLI needs access to the files
      - uses: BogDAAAMN/deta-deploy-action@v1.0.1
        with:
          deta-access-token: ${{ secrets.DETA_TOKEN }} #Deta access token https://docs.deta.sh/docs/cli/auth
          deta-name: "micro-name" #Deta Micro name https://docs.deta.sh/docs/cli/commands/#deta-clone
          deta-project: "project-name" #Optional: Deta project name https://docs.deta.sh/docs/cli/commands/#deta-clone
          deta-project-dir: "other-dir" #Optional: directory to be deployed on Deta. Default is the root "."
```
