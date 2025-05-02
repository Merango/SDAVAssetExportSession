# SDAVAssetExportSession: Advanced Media Transcoding for iOS

## Project Overview

SDAVAssetExportSession is a powerful, flexible alternative to Apple's `AVAssetExportSession` for video and audio asset transcoding in iOS applications. It provides developers with granular control over media export settings, addressing the limitations of preset-based export methods.

### Key Features

- **Customizable Media Export**: Unlike the standard `AVAssetExportSession`, this library allows full customization of video and audio encoding settings.
- **Flexible Configuration**: Set precise parameters for video and audio tracks, including:
  - Video codec
  - Resolution
  - Bitrate
  - Compression properties
  - Audio format
  - Sample rate
  - Number of channels
- **Asynchronous Export**: Perform media transcoding operations without blocking the main thread
- **Error Handling**: Comprehensive status and error reporting
- **Network Optimization**: Option to optimize output for network use

### Problem Solved

Standard `AVAssetExportSession` limits developers to predefined presets, making it challenging to meet specific media encoding requirements. SDAVAssetExportSession eliminates these constraints by providing a developer-friendly interface for low-level media transformation, simplifying complex video and audio processing tasks.

## Getting Started, Installation, and Setup

### Prerequisites

- iOS 6.0 or later
- Xcode
- ARC (Automatic Reference Counting) enabled

### Installation

#### CocoaPods

Add the following to your `Podfile`:

```ruby
pod 'SDAVAssetExportSession'
```

Then run:

```bash
pod install
```

#### Manual Installation

1. Clone the repository or download the source files.
2. Add `SDAVAssetExportSession.h` and `SDAVAssetExportSession.m` to your project.
3. Import the header in your Objective-C file:

```objective-c
#import "SDAVAssetExportSession.h"
```

### Quick Start

Here's a basic example of how to use `SDAVAssetExportSession` to export a video with custom settings:

```objective-c
// Assuming you have an AVAsset named 'anAsset'
SDAVAssetExportSession *encoder = [SDAVAssetExportSession.alloc initWithAsset:anAsset];

// Configure output file
encoder.outputFileType = AVFileTypeMPEG4;
encoder.outputURL = outputFileURL;

// Configure video settings
encoder.videoSettings = @{
    AVVideoCodecKey: AVVideoCodecH264,
    AVVideoWidthKey: @1920,
    AVVideoHeightKey: @1080,
    AVVideoCompressionPropertiesKey: @{
        AVVideoAverageBitRateKey: @6000000,
        AVVideoProfileLevelKey: AVVideoProfileLevelH264High40,
    },
};

// Configure audio settings
encoder.audioSettings = @{
    AVFormatIDKey: @(kAudioFormatMPEG4AAC),
    AVNumberOfChannelsKey: @2,
    AVSampleRateKey: @44100,
    AVEncoderBitRateKey: @128000,
};

// Export the video
[encoder exportAsynchronouslyWithCompletionHandler:^{
    switch (encoder.status) {
        case AVAssetExportSessionStatusCompleted:
            NSLog(@"Video export succeeded");
            break;
        case AVAssetExportSessionStatusCancelled:
            NSLog(@"Video export cancelled");
            break;
        default:
            NSLog(@"Video export failed with error: %@", encoder.error);
            break;
    }
}];
```

### Customization

`SDAVAssetExportSession` provides full control over audio and video export settings, allowing you to customize:
- Video codec
- Resolution
- Bitrate
- Audio format
- Channels
- Sample rate

Refer to the Apple documentation for available keys and values for `videoSettings` and `audioSettings`.

## Additional Notes

### Performance Considerations

The library provides fine-grained control over video and audio encoding, which can impact performance depending on the complexity of your settings. When configuring export sessions, consider the following:

- Custom video and audio settings may increase processing time
- Higher bitrates and resolution will consume more computational resources
- Network optimization can affect overall export performance

### Compatibility

- Designed for iOS platforms using AVFoundation
- Requires iOS 7.0 and above
- Compatible with both Swift and Objective-C projects

### Error Handling

Always check the `status` and `error` properties after export completion. Possible statuses include:
- `AVAssetExportSessionStatusCompleted`
- `AVAssetExportSessionStatusFailed`
- `AVAssetExportSessionStatusCancelled`

### Memory Management

- The export session is not retained after completion
- Ensure strong references are maintained during asynchronous export
- Use weak references in completion handlers to prevent retain cycles

### Logging and Debugging

For troubleshooting, implement comprehensive logging in the completion handler to capture export status and potential errors. Example:

```objective-c
[encoder exportAsynchronouslyWithCompletionHandler:^{
    switch (encoder.status) {
        case AVAssetExportSessionStatusCompleted:
            NSLog(@"Export succeeded");
            break;
        case AVAssetExportSessionStatusFailed:
            NSLog(@"Export failed: %@", encoder.error);
            break;
        case AVAssetExportSessionStatusCancelled:
            NSLog(@"Export was cancelled");
            break;
        default:
            break;
    }
}];
```

## Contributing

We welcome contributions to SDAVAssetExportSession! By contributing, you help improve this library for the entire community.

### How to Contribute

1. **Fork the Repository**: Create a fork of the project on GitHub.

2. **Create a Branch**: 
   - Make a new branch for your feature or bugfix
   - Use a clear, descriptive name for your branch
   - Example: `feature/add-new-export-option` or `bugfix/resolve-encoding-issue`

3. **Code Guidelines**:
   - Follow existing Objective-C coding conventions in the project
   - Maintain clean, readable, and well-documented code
   - Ensure new code matches the project's existing style

4. **Testing**:
   - Add or update tests for any new functionality
   - Ensure all existing tests pass before submitting a pull request
   - Test on different iOS versions and device configurations when possible

5. **Pull Request Process**:
   - Provide a clear, descriptive title for your pull request
   - Include a detailed description of your changes
   - Explain the motivation and context of your contribution

### Reporting Issues

- Use GitHub Issues to report bugs or suggest enhancements
- Include a clear description and steps to reproduce the issue
- Provide your environment details (iOS version, Xcode version)
- If applicable, include sample code demonstrating the problem

### Code of Conduct

- Be respectful and considerate of other contributors
- Collaborate constructively
- Help maintain a welcoming and inclusive community

### Questions?

If you have any questions about contributing, please open an issue for discussion.

## License

This project is licensed under the MIT License. 

#### License Details
- Full license text is available in the [LICENSE](LICENSE) file
- Copyright (c) 2013 Olivier Poitrey

#### Key Permissions
- Commercial use
- Modification
- Distribution
- Private use

#### Conditions
- License and copyright notice must be included
- The software is provided "as is" without warranties

For complete license terms, please refer to the full [LICENSE](LICENSE) file in the repository.