<!DOCTYPE html>
<html lang="fr" data-theme="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Application de Notes avec Catégories</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <button id="theme-toggle" class="theme-toggle" aria-label="Changer de thème">
        <!-- Icône de soleil (mode clair) -->
        <svg id="sun-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <circle cx="12" cy="12" r="5"></circle>
            <line x1="12" y1="1" x2="12" y2="3"></line>
            <line x1="12" y1="21" x2="12" y2="23"></line>
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
            <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
            <line x1="1" y1="12" x2="3" y2="12"></line>
            <line x1="21" y1="12" x2="23" y2="12"></line>
            <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
            <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
        </svg>
        <!-- Icône de lune (mode sombre) -->
        <svg id="moon-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" style="display: none;">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
        </svg>
        <span id="theme-text">Mode sombre</span>
    </button>

    <div class="container">
        <header>
            <h1>Mes Notes</h1>
            <p class="subtitle">Une application simple pour gérer vos notes et catégories</p>
        </header>

        <div class="app-layout">
            <div class="categories-sidebar">
                <div class="sidebar-header">
                    <h3>Catégories</h3>
                    <button id="create-category-btn" class="btn secondary btn-small">
                        <span class="icon">+</span>
                    </button>
                </div>
                <div id="categories-sidebar" class="categories-list">
                    <div class="category-item active" data-id="all">
                        Toutes les notes
                    </div>
                    <div class="category-item" data-id="uncategorized">
                        Sans catégorie
                    </div>
                    <!-- Les catégories seront ajoutées ici dynamiquement -->
                </div>
            </div>

            <div class="notes-section">
                <div class="notes-actions">
                    <div class="search-container">
                        <input type="text" id="search-input" placeholder="Rechercher une note..." class="search-input">
                        <button id="search-btn" class="btn secondary search-btn">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <circle cx="11" cy="11" r="8"></circle>
                                <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                            </svg>
                        </button>
                    </div>
                    <button id="create-note-btn" class="btn primary create-btn">
                        <span class="icon">+</span> Nouvelle Note
                    </button>
                </div>
                <div id="notes-container" class="notes-grid">
                    <!-- Les notes seront ajoutées ici dynamiquement -->
                </div>
                <div id="empty-state" class="empty-state">
                    <p>Vous n'avez pas encore de notes.</p>
                    <p>Cliquez sur "Nouvelle Note" pour commencer.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de création de note -->
    <div id="create-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Créer une nouvelle note</h2>
                <button class="close-btn">&times;</button>
            </div>
            <form id="note-form">
                <div class="form-group">
                    <label for="note-title">Titre</label>
                    <input type="text" id="note-title" placeholder="Titre de la note" required>
                </div>
                <div class="form-group">
                    <label for="note-content">Contenu</label>
                    <textarea id="note-content" placeholder="Contenu de votre note..." required></textarea>
                </div>
                <div class="form-group">
                    <label for="note-category">Catégorie</label>
                    <select id="note-category">
                        <option value="">Sans catégorie</option>
                        <!-- Les catégories seront ajoutées ici dynamiquement -->
                    </select>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn secondary" id="cancel-btn">Annuler</button>
                    <button type="submit" class="btn primary">Créer</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal de visualisation de note -->
    <div id="view-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="view-title"></h2>
                <button class="close-btn">&times;</button>
            </div>
            <div class="note-metadata">
                <span id="view-date"></span>
                <span id="view-category" class="category-badge"></span>
            </div>
            <div class="note-content" id="view-content"></div>
            <div class="modal-actions">
                <button class="btn secondary" id="edit-btn">Modifier</button>
                <button class="btn danger" id="delete-btn">Supprimer</button>
            </div>
        </div>
    </div>

    <!-- Modal de modification de note -->
    <div id="edit-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Modifier la note</h2>
                <button class="close-btn">&times;</button>
            </div>
            <form id="edit-form">
                <div class="form-group">
                    <label for="edit-title">Titre</label>
                    <input type="text" id="edit-title" placeholder="Titre de la note" required>
                </div>
                <div class="form-group">
                    <label for="edit-content">Contenu</label>
                    <textarea id="edit-content" placeholder="Contenu de votre note..." required></textarea>
                </div>
                <div class="form-group">
                    <label for="edit-category">Catégorie</label>
                    <select id="edit-category">
                        <option value="">Sans catégorie</option>
                        <!-- Les catégories seront ajoutées ici dynamiquement -->
                    </select>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn secondary" id="cancel-edit-btn">Annuler</button>
                    <button type="submit" class="btn primary">Mettre à jour</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal de suppression de note -->
    <div id="delete-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Supprimer la note</h2>
                <button class="close-btn">&times;</button>
            </div>
            <p>Êtes-vous sûr de vouloir supprimer la note "<span id="delete-note-title"></span>" ?</p>
            <p>Cette action est irréversible.</p>
            <div class="modal-actions">
                <button class="btn secondary" id="cancel-delete-btn">Annuler</button>
                <button class="btn danger" id="confirm-delete-btn">Supprimer</button>
            </div>
        </div>
    </div>

    <!-- Modal de création de catégorie -->
    <div id="category-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Créer une nouvelle catégorie</h2>
                <button class="close-btn">&times;</button>
            </div>
            <form id="category-form">
                <div class="form-group">
                    <label for="category-name">Nom de la catégorie</label>
                    <input type="text" id="category-name" placeholder="Nom de la catégorie" required>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn secondary" id="cancel-category-btn">Annuler</button>
                    <button type="submit" class="btn primary">Créer</button>
                </div>
            </form>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
