# Documentation

## Documentation is included in the Documentation folder

# REFrameWork Template

## Robotic Enterprise Framework

- Built on top of **Transactional Business Process** template
- Uses **State Machine** layout for the phases of the automation project
- Offers high-level **logging**, **exception handling**, and **recovery**
- Keeps external settings in **Config.xlsx** file and **Orchestrator assets**
- Pulls credentials from **Orchestrator assets** and **Windows Credential Manager**
- Gets transaction data from **Orchestrator queue** and updates back status
- Takes **screenshots** in case of system exceptions

## How It Works

### INITIALIZE PROCESS
- `./Framework/InitiAllSettings` - Load configuration data from **Config.xlsx** file and from assets
- `./Framework/GetAppCredential` - Retrieve credentials from **Orchestrator assets** or local **Windows Credential Manager**
- `./Framework/InitiAllApplications` - Open and login to applications used throughout the process

### GET TRANSACTION DATA
- `./Framework/GetTransactionData` - Fetches transactions from an **Orchestrator queue** defined by `Config("OrchestratorQueueName")` or any other configured data source

### PROCESS TRANSACTION
- Process - Process transaction and invoke other workflows related to the process being automated
- `./Framework/SetTransactionStatus` - Updates the status of the processed transaction (Orchestrator transactions by default): Success, Business Rule Exception, or System Exception

### END PROCESS
- `./Framework/CloseAllApplications` - Logs out and closes applications used throughout the process

## For New Project
1. Check the **Config.xlsx** file and add/customize any required fields and values
2. Implement `InitiAllApplications.xaml` and `CloseAllApplications.xaml` workflows, linking them in the **Config.xlsx** fields
3. Implement `GetTransactionData.xaml` and `SetTransactionStatus.xaml` according to the transaction type being used (Orchestrator queues by default)
4. Implement `Process.xaml` workflow and invoke other workflows related to the process being automated

