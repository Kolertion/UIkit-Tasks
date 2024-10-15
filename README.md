import UIKit

class ViewController: UIViewController {

    // MARK: - UI Elements
    private let titleLabel = UILabel()
    private let descriptionLabel = UILabel()
    private let textField = UITextField()
    private let actionButton = UIButton(type: .system)
    private let resultLabel = UILabel()

    // MARK: - Lifecycle
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
        setupActions()
    }

    // MARK: - UI Setup
    private func setupUI() {
        view.backgroundColor = .white
        
        setupTitleLabel()
        setupDescriptionLabel()
        setupTextField()
        setupActionButton()
        setupResultLabel()
        
        layoutUI()
    }
    
    private func setupTitleLabel() {
        titleLabel.text = "Reverse Words"
        titleLabel.font = .systemFont(ofSize: 24, weight: .bold)
        titleLabel.textAlignment = .center
    }
    
    private func setupDescriptionLabel() {
        descriptionLabel.text = "This application will reverse your words.\nPlease type text below"
        descriptionLabel.font = .systemFont(ofSize: 14)
        descriptionLabel.textAlignment = .center
        descriptionLabel.numberOfLines = 0
    }
    
    private func setupTextField() {
        textField.placeholder = "Text to reverse"
        textField.borderStyle = .roundedRect
    }
    
    private func setupActionButton() {
        actionButton.setTitle("Reverse", for: .normal)
        actionButton.backgroundColor = .systemBlue
        actionButton.setTitleColor(.white, for: .normal)
        actionButton.layer.cornerRadius = 8
        actionButton.isEnabled = false
    }
    
    private func setupResultLabel() {
        resultLabel.textAlignment = .center
        resultLabel.numberOfLines = 0
    }
    
    private func layoutUI() {
        let stackView = UIStackView(arrangedSubviews: [
            titleLabel, descriptionLabel, textField, actionButton, resultLabel
        ])
        stackView.axis = .vertical
        stackView.spacing = 20
        stackView.translatesAutoresizingMaskIntoConstraints = false
        
        view.addSubview(stackView)
        
        NSLayoutConstraint.activate([
            stackView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 20),
            stackView.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            stackView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            actionButton.heightAnchor.constraint(equalToConstant: 50)
        ])
    }

    // MARK: - Actions
    private func setupActions() {
        textField.addTarget(self, action: #selector(textFieldDidChange), for: .editingChanged)
        actionButton.addTarget(self, action: #selector(actionButtonTapped), for: .touchUpInside)
    }
    
    @objc private func textFieldDidChange() {
        actionButton.isEnabled = !textField.text!.isEmpty
    }
    
    @objc private func actionButtonTapped() {
        if actionButton.title(for: .normal) == "Reverse" {
            reverseText()
        } else {
            clearText()
        }
    }
    
    private func reverseText() {
        guard let text = textField.text, !text.isEmpty else { return }
        resultLabel.text = String(text.reversed())
        actionButton.setTitle("Clear", for: .normal)
    }
    
    private func clearText() {
        textField.text = ""
        resultLabel.text = ""
        actionButton.setTitle("Reverse", for: .normal)
        actionButton.isEnabled = false
    }
}
