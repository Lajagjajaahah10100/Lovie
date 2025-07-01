# Lovie
My dating app
import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select';
import { Textarea } from '@/components/ui/textarea';
import { MBTI_TYPES, ZODIAC_SIGNS } from '@/constants/mbti';
import { User } from '@/types/user';

interface ProfileSetupProps {
  onComplete: (user: Partial<User>) => void;
}

const ProfileSetup: React.FC<ProfileSetupProps> = ({ onComplete }) => {
  const [formData, setFormData] = useState({
    name: '',
    age: '',
    email: '',
    className: '',
    mbtiType: '',
    zodiacSign: '',
    bio: '',
    location: '',
  });

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    
    const userData: Partial<User> = {
      name: formData.name,
      age: parseInt(formData.age),
      email: formData.email,
      className: formData.className,
      mbtiType: formData.mbtiType,
      zodiacSign: formData.zodiacSign,
      bio: formData.bio,
      location: formData.location,
      interests: [], // Empty array instead of parsed interests
      isOnline: true,
    };

    onComplete(userData);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-50 to-purple-50 p-4">
      <div className="max-w-md mx-auto">
        <Card className="shadow-lg">
          <CardHeader className="text-center">
            <CardTitle className="text-2xl font-bold text-purple-800">
              💕 Loveable
            </CardTitle>
            <p className="text-gray-600">Жинхэнэ хайраа олоорой</p>
          </CardHeader>
          <CardContent>
            <form onSubmit={handleSubmit} className="space-y-4">
              <div>
                <Label htmlFor="name">Нэр</Label>
                <Input
                  id="name"
                  value={formData.name}
                  onChange={(e) => setFormData({...formData, name: e.target.value})}
                  placeholder="Таны нэр"
                  required
                />
              </div>

              <div>
                <Label htmlFor="age">Нас</Label>
                <Input
                  id="age"
                  type="number"
                  value={formData.age}
                  onChange={(e) => setFormData({...formData, age: e.target.value})}
                  placeholder="Таны нас"
                  required
                />
              </div>

              <div>
                <Label htmlFor="className">Анги</Label>
                <Input
                  id="className"
                  value={formData.className}
                  onChange={(e) => setFormData({...formData, className: e.target.value})}
                  placeholder="Жишээ: 12А анги"
                  required
                />
              </div>

              <div>
                <Label htmlFor="mbti">MBTI төрөл</Label>
                <Select onValueChange={(value) => setFormData({...formData, mbtiType: value})}>
                  <SelectTrigger>
                    <SelectValue placeholder="MBTI төрлөө сонгоно уу" />
                  </SelectTrigger>
                  <SelectContent>
                    {MBTI_TYPES.map((type) => (
                      <SelectItem key={type.value} value={type.value}>
                        {type.label}
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>

              <div>
                <Label htmlFor="zodiac">Зурхайн тэмдэг</Label>
                <Select onValueChange={(value) => setFormData({...formData, zodiacSign: value})}>
                  <SelectTrigger>
                    <SelectValue placeholder="Зурхайн тэмдгээ сонгоно уу" />
                  </SelectTrigger>
                  <SelectContent>
                    {ZODIAC_SIGNS.map((sign) => (
                      <SelectItem key={sign.value} value={sign.value}>
                        {sign.label}
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>

              <div>
                <Label htmlFor="bio">Тухай</Label>
                <Textarea
                  id="bio"
                  value={formData.bio}
                  onChange={(e) => setFormData({...formData, bio: e.target.value})}
                  placeholder="Өөрийн тухай товчхон бичнэ үү..."
                  rows={3}
                />
              </div>

              <Button type="submit" className="w-full bg-purple-600 hover:bg-purple-700">
                Профайл үүсгэх
              </Button>
            </form>
          </CardContent>
        </Card>
      </div>
    </div>
  );
};

export default ProfileSetup;
