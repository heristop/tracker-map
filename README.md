# TreePulse

**TreePulse** is a versatile project management tool designed to track the progress of various types of projects and processes. Initially created for monitoring the migration of Information Systems or applications, **TreePulse** helps you visualize and monitor the status of your projects effectively.

![screenshot](/public/screenshot.png)

## ✨ Features

- **Migration Tracking**: Monitor the migration progress of your Information Systems or applications.
- **Task Management**: Track tasks, subtasks, and their statuses.
- **Bug Tracking**: Manage bug reports, assign them to developers, and monitor their resolution.
- **Production Management**: Visualize production stages, quality control statuses, and inventory levels.
- **Sales and Marketing**: Follow marketing campaigns, sales opportunities, and contracts.
- **HR Management**: Track recruitment processes, employee training programs, and more.
- **Customizable Statuses**: Define and customize statuses to fit your specific workflow.
- **Import/Export**: Import project data from JSON files and export current project data for backup or sharing.
- **And more...**

## 🛠️ Installation

To install and run **TreePulse** locally, follow these steps:

1. Clone the repository:

    ```bash
    git clone https://github.com/heristop/tree-pulse.git
    cd tree-pulse
    ```

2. Install dependencies:

    ```bash
    pnpm install
    ```

3. Start the development server:

    ```bash
    pnpm run dev
    ```

4. Open your browser and navigate to `http://localhost:3000`.

## 📚 Usage

### Loading Configuration

- **From Local Storage**: If a saved configuration is present in local storage, TreePulse will automatically load it upon startup. This ensures your previous session's data is readily available.
- **From API**: If no local configuration is found, you can easily load a sample configuration by clicking the "Load Sample Data" button. This allows you to quickly start working with a predefined setup.

### Importing and Exporting Data

- **Import**:
  - Navigate to the configuration panel.
  - Click the upload button to import project data from a JSON file.
  - Select your JSON file from the file dialog. The imported data will replace the current configuration, allowing you to seamlessly continue your work.
- **Export**:
  - In the configuration panel, click the save button.
  - This will export the current project data to a JSON file, preserving your work and enabling easy sharing and backup.

### Managing Projects

- **Adding/Updating Statuses**: 
  - Open the configuration panel to manage statuses.
  - You can add new statuses to categorize tasks more effectively, update existing ones to reflect changes in your workflow, or remove obsolete statuses.
- **Updating Tasks**: 
  - Click on any task to cycle through its statuses.
  - This intuitive interface allows for quick updates, ensuring your project board accurately reflects the current state of each task.

### JSON Configuration Format

The JSON configuration file should adhere to the following structure to be compatible with TreePulse:

```json
[
  {
    "key": "project-1",
    "name": "Project 1",
    "children": [
      {
        "key": "task-1",
        "name": "Task 1",
        "status": "In Progress",
        "children": []
      },
      {
        "key": "task-2",
        "name": "Task 2",
        "status": "Done",
        "children": []
      }
    ]
  },
  {
    "key": "project-2",
    "name": "Project 2",
    "children": []
  }
]
```

- `key`: A unique identifier for the section or task, ensuring each element is distinct.
- `name`: The name of the section or task, providing a clear label for easy identification.
- `status`: The current status of the section or task (e.g., "In Progress", "Done"), allowing for effective tracking and categorization.
- `children`: An array of nested sections or tasks, supporting hierarchical project structures.
- `isCollapsed` (optional): A boolean flag indicating whether the section should be collapsed, helping to manage the visibility of complex structures.

By following this guide, you can effectively utilize TreePulse to manage your projects, import/export data seamlessly, and maintain a well-organized JSON configuration.

## 📄 License

This project is licensed under the MIT License.

## 💬 Feedback and Contributions

We welcome feedback and contributions! If you have any suggestions or encounter any issues, please feel free to open an issue or submit a pull request.

![Logo](/public/apple-touch-icon.png)
