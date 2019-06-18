const inquirer = require('inquirer');
const fs = require('fs');

const CHOICES = fs.readdirSync(`${__dirname}`);
const path = require('path');
const mkdirp = require('mkdirp-promise');


const QUESTIONS = [
   {
    name: 'project-name',
    type: 'input',
    message: 'API name:',
    validate: function (input) {
      if (/^([A-Za-z\-\_\d])+$/.test(input)) return true;
      else return 'Project name may only include letters, numbers, underscores and hashes.';
    }
  }
  ,
  {
    name: 'end-point-name',
    type: 'input',
    message: 'End Point name:',
    validate: function (input) {
      if (/^([A-Za-z\-\_\d])+$/.test(input)) return true;
      else return 'End Point name may only include letters, numbers, underscores and hashes.';
    }
  }

];


const CURR_DIR = process.cwd();

inquirer.prompt(QUESTIONS)
  .then(answers => { 
   // const projectChoice = answers['project-choice'];
    const projectName = answers['project-name'];
    const endpointname = answers['end-point-name'];
   
    let dirs = [
      "Web-Services/"+`${projectName}`+"/"+`${endpointname}`+"/Response",
      "Web-Services/"+`${projectName}`+"/"+`${endpointname}`+"/TestScripts",
      "Web-Services/"+`${projectName}`+"/"+`${endpointname}`+"/TestData",
    ];

    makeAllDirs(__dirname, dirs).then(() => {
     console.log("done...")
    }).catch(err => {
      console.log(err)
   });

  });

  function makeAllDirs(root, list) {
    return list.reduce((p, item) => {
        return p.then(() => {
            return mkdirp(path.join(root, item));
        });
    }, Promise.resolve());
}

