Tired of spending an hour trying to set up a simple typescript project... me too. 

Add this to your .zshrc file. 

Run it. 
`setup_ts_project my-project-name`

Done.

```
setup_ts_project() {
  # Check if a project name was provided
  if [ -z "$1" ]; then
    echo "Please provide a project name."
    return 1
  fi

  # Create and navigate to project directory
  mkdir "$1" && cd "$1"

  # Initialize Node.js project
  npm init -y

  # Install dependencies
  npm install --save-dev typescript ts-node prettier

  # Create TypeScript config
  npx tsc --init

  # Create Prettier config
  echo '{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2
}' > .prettierrc

  # Add scripts to package.json
  npm pkg set scripts.start="ts-node"
  npm pkg set scripts.format="prettier --write ."

  # Create sample TypeScript file
  echo 'console.log("Hello, TypeScript!");' > index.ts

  # Create VS Code settings for format on save
  mkdir .vscode
  echo '{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}' > .vscode/settings.json

  echo "TypeScript project $1 has been set up successfully!"
}
```
