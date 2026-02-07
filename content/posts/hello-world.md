---
title: "Hello, World"
date: 2026-02-07
draft: false
tags: ["csharp", "dotnet"]
---

First post. Testing syntax highlighting with a simple C# example.

<!--more-->

## A basic async HTTP client

```csharp
using System.Net.Http;
using System.Text.Json;

namespace Blog.Examples;

public record Post(int Id, string Title, string Body);

public static class ApiClient
{
    private static readonly HttpClient _http = new();

    public static async Task<Post?> GetPostAsync(int id)
    {
        var response = await _http.GetAsync(
            $"https://jsonplaceholder.typicode.com/posts/{id}");

        response.EnsureSuccessStatusCode();

        var json = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<Post>(json, new JsonSerializerOptions
        {
            PropertyNameCaseInsensitive = true
        });
    }

    public static async Task Main(string[] args)
    {
        var post = await GetPostAsync(1);
        Console.WriteLine($"[{post?.Id}] {post?.Title}");
    }
}
```

If the highlighting above renders correctly, we're in business.
