# Changelog

Notable changes to this project will be documented in this file.

## 2024-01-09

### Modified
#### Configuration Changes
- Updated Docker configurations:
  - Changes to `Dockerfile`:
    - Improved layer caching by separating dependency and code layers
  - Updates to `docker-compose.yml` and `docker-compose.cpu.yml`:
    - Removed commit lock from model fetching to allow automatic model updates from HF
    - Added git index lock cleanup

#### API Changes
- Modified `api/src/main.py`
- Updated TTS service implementation in `api/src/services/tts.py`:
  - Added device management for better resource control:
    - Voices are now copied from model repository to api/src/voices directory for persistence
  - Refactored voice pack handling:
    - Removed static voice pack dictionary
    - On-demand voice loading from disk
  - Added model warm-up functionality:
    - Model now initializes with a dummy text generation
    - Uses default voice (af.pt) for warm-up
    - Model is ready for inference on first request